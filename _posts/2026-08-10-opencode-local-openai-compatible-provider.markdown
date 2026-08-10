---
layout: post
title: "opencode에 로컬 vLLM · Ollama 서버 연결하기 (OpenAI 호환 provider 설정)"
date: 2026-08-10 10:00:00 +0900
categories: opencode
---

opencode에서 직접 돌리는 로컬 LLM 서버를 붙이려다 시간을 꽤 썼다. 터미널 CLI나 IDE의 연결 메뉴(`/connect`)에서는 Ollama Cloud, OpenAI API Key 같은 항목만 보여서, 내 서버 주소를 넣을 자리가 없는 것처럼 보인다. 검색해도 관련 글이 잘 나오지 않아서, 결론부터 적어둔다.

**메뉴로는 안 되고, 설정 파일을 직접 편집하면 된다.** OpenAI 호환 엔드포인트만 있으면 vLLM이든 Ollama든 llama.cpp든 전부 붙는다.

## 결론: 설정 파일 하나만 만들면 된다

전역 설정 파일은 여기다.

```
~/.config/opencode/opencode.jsonc
```

프로젝트별로 적용하려면 프로젝트 루트에 `opencode.json`을 두어도 된다. 파일이 없으면 새로 만들면 된다.

내가 쓰고 있는 실제 설정은 이게 전부다.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "deepseek-v4-spark": {
      "name": "deepseek-v4-spark",
      "npm": "@ai-sdk/openai-compatible",
      "options": {
        "baseURL": "http://100.x.x.x:8888/v1"
      },
      "models": {
        "deepseek-v4-flash-0731": {
          "name": "deepseek-v4-flash-0731"
        }
      }
    }
  }
}
```

이렇게만 해두면 opencode에서 모델을 고를 때 아래 형식으로 지정할 수 있다.

```
deepseek-v4-spark/deepseek-v4-flash-0731
```

즉 `provider키/모델키` 형태다. 이게 핵심이다.

## 각 항목이 무슨 뜻인지

- **`provider` 아래의 키** (`deepseek-v4-spark`) — 내가 정하는 provider 식별자. 모델 지정할 때 앞부분이 된다.
- **`npm`** — `@ai-sdk/openai-compatible`을 쓴다. `/v1/chat/completions` 규격을 쓰는 서버는 전부 이걸로 붙는다. 별도로 설치할 필요는 없고, opencode가 알아서 받아온다.
- **`options.baseURL`** — 서버 주소. **끝에 `/v1`을 반드시 붙인다.** 이걸 빠뜨려서 헤매는 경우가 많다.
- **`models` 아래의 키** — 서버가 실제로 서빙하는 모델 ID. 여기가 두 번째 함정인데, 아래에서 따로 설명한다.
- **`name`** — 화면에 표시되는 이름이라 아무렇게나 적어도 동작한다.

API key 항목이 아예 없는 것도 눈여겨볼 만하다. 인증 없이 열어둔 내부망 서버라면 `apiKey`를 안 써도 그냥 붙는다. 메뉴에서 API Key를 요구하는 것처럼 보여서 "키가 없으면 못 쓰나" 싶었는데, 설정 파일에서는 생략해도 된다.

## 서버가 서빙하는 모델 ID 확인하기

`models`의 키는 **서버가 응답하는 모델 ID와 정확히 같아야 한다.** 허깅페이스 경로(`deepseek-ai/DeepSeek-V4-Flash-0731`)를 그대로 적으면 안 된다. 확인은 curl 한 줄이면 된다.

```bash
curl -s http://100.x.x.x:8888/v1/models | python3 -m json.tool
```

응답은 이런 식이다.

```json
{
  "object": "list",
  "data": [
    {
      "id": "deepseek-v4-flash-0731",
      "object": "model",
      "owned_by": "vllm",
      "root": "deepseek-ai/DeepSeek-V4-Flash-0731",
      "max_model_len": 1048576
    }
  ]
}
```

여기서 설정에 넣어야 하는 값은 `root`가 아니라 **`id`** 인 `deepseek-v4-flash-0731`이다. `root`는 원본 모델 경로일 뿐이다. 그리고 이 curl이 정상 응답한다는 것 자체가 "서버는 문제없다"는 확인이 되므로, 연결이 안 될 때 가장 먼저 해볼 일이기도 하다.

참고로 `max_model_len`이 1,048,576이니 이 서버는 1M 컨텍스트를 지원한다. 컨텍스트 한도를 opencode에 명시하고 싶으면 `limit`을 추가하면 된다.

```jsonc
"models": {
  "deepseek-v4-flash-0731": {
    "name": "deepseek-v4-flash-0731",
    "limit": {
      "context": 1048576,
      "output": 65536
    }
  }
}
```

## Ollama 로컬 서버 붙이기

Ollama도 원리가 똑같다. Ollama는 `11434` 포트에서 OpenAI 호환 API를 제공하므로 `baseURL`만 바꿔주면 된다.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "ollama": {
      "name": "Ollama (local)",
      "npm": "@ai-sdk/openai-compatible",
      "options": {
        "baseURL": "http://localhost:11434/v1"
      },
      "models": {
        "qwen3.6:35b": { "name": "qwen3.6:35b" },
        "gemma4:31b": { "name": "gemma4:31b" }
      }
    }
  }
}
```

설치된 모델 목록은 이렇게 확인한다. 여기 나오는 `id`를 그대로 `models` 키로 쓰면 된다. 태그(`:35b`)까지 포함해야 한다.

```bash
curl -s http://localhost:11434/v1/models | python3 -c "import json,sys; [print(m['id']) for m in json.load(sys.stdin)['data']]"
```

Ollama에서 도구 호출(tool call)이 잘 안 되면 `num_ctx`를 16k~32k 정도로 올려보라는 것이 공식 문서의 안내다. 코딩 에이전트로 쓸 때는 컨텍스트가 기본값으로는 부족한 경우가 많다.

## 여러 개를 동시에 등록해도 된다

`provider` 아래에 나란히 적으면 여러 서버를 함께 등록할 수 있다.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "deepseek-v4-spark": {
      "name": "deepseek-v4-spark",
      "npm": "@ai-sdk/openai-compatible",
      "options": { "baseURL": "http://100.x.x.x:8888/v1" },
      "models": { "deepseek-v4-flash-0731": { "name": "deepseek-v4-flash-0731" } }
    },
    "ollama": {
      "name": "Ollama (local)",
      "npm": "@ai-sdk/openai-compatible",
      "options": { "baseURL": "http://localhost:11434/v1" },
      "models": { "qwen3.6:35b": { "name": "qwen3.6:35b" } }
    }
  }
}
```

인증이 필요한 서버라면 API 키를 환경변수로 빼서 참조할 수 있다. 설정 파일에 키를 직접 적지 않아도 된다.

```jsonc
"options": {
  "baseURL": "https://api.example.com/v1",
  "apiKey": "{env:MY_API_KEY}"
}
```

## 잘 안 될 때 확인할 것

1. **`baseURL` 끝에 `/v1`이 있는가.** 가장 흔한 실수다.
2. **`models` 키가 서버의 `id`와 정확히 일치하는가.** 허깅페이스 경로를 적지 않았는지 확인한다.
3. **curl로 `/v1/models`가 응답하는가.** 응답이 없으면 opencode 문제가 아니라 서버나 네트워크 문제다.
4. **`.jsonc` 확장자를 썼다면 주석은 괜찮지만, `.json`으로 저장했다면 주석과 마지막 쉼표를 제거한다.**
5. **원격 서버라면 방화벽과 바인딩 주소를 확인한다.** vLLM을 `127.0.0.1`에 바인딩해두면 외부에서 접속되지 않는다. `--host 0.0.0.0`으로 띄워야 한다.

## 남는 이야기

내 서버는 Tailscale로 묶인 내부망에 있어서 주소가 `100.x.x.x` 대역이다. opencode 입장에서는 그냥 HTTP로 접근 가능한 주소일 뿐이라, Tailscale이든 LAN이든 도메인이든 아무 상관이 없었다. 이 점을 알고 나니 오히려 구성이 단순해졌다. 결국 필요한 건 "OpenAI 호환 엔드포인트 하나"뿐이다.

메뉴에 없다고 해서 지원하지 않는 기능이라고 생각하기 쉬운데, 실제로는 설정 파일 쪽이 훨씬 자유롭다. 비슷한 상황에서 헤매는 사람이 있다면 이 글이 도움이 되었으면 한다.

[opencode 공식 문서 - Providers](https://opencode.ai/docs/providers/)
