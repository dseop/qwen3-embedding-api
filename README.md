# qwen3-embedding-api

Qwen3-Embedding-0.6B 모델 기반 문장 임베딩 및 RESTful API 서빙 포트폴리오 예제입니다. FastAPI를 이용하여 텍스트 임베딩 및 유사도 분석을 지원합니다.

## 주요 특징
- **Qwen3-Embedding-0.6B** 모델 탑재
- **FastAPI** 기반 RESTful API 서버
- **문장 임베딩**, **코사인 유사도 분석** 제공
- 예시 코드 및 사용법 안내 포함

## 설치 및 실행 방법
```bash
# 저장소 클론
$ git clone https://github.com/dseop/qwen3-embedding-api.git
$ cd qwen3-embedding-api

# 의존성 설치
$ pip install -r requirements.txt

# 서버 실행
$ uvicorn main:app --reload
```

## API 예시
### 임베딩 추출
```
POST /embed
{
  "text": "테스트 문장"
}
```

응답 예시:
```
{
  "embedding": [0.123, 0.456, ...]
}
```

### 유사도 분석
```
POST /similarity
{
  "text1": "문장 1",
  "text2": "문장 2"
}
```

응답 예시:
```
{
  "similarity": 0.92
}
```

## 참고
- [FastAPI 공식 문서](https://fastapi.tiangolo.com/)
- [Qwen3 모델 공식 GitHub](https://github.com/QwenLM/Qwen3)
