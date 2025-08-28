# qwen3-embedding-api
Qwen3-Embedding-0.6B 모델 기반 문장 임베딩 및 RESTful API 구현.

- Colab에서 모델을 로딩하고 API 엔드포인트로 사용할 수 있도록 구현했습니다.
- 문장 리스트를 입력 받아 문장간 유사도 행렬을 출력합니다.
- 배치 사이즈를 최대 32로 두었는데, colab의 성능에 따라 높일 수 있습니다.
- 문장의 분류가 가능하다면 클러스터링 후 전달하는 것이 권장됩니다.

## 주요 구현 내용
- **Qwen3-Embedding-0.6B** (Huggingface) 모델 기반 임베딩
- **Google Colab에서** 모델 로딩 및 실습 환경 구성
- **FastAPI** 기반 REST API 서버 제작 및 pyngrok 외부 공개
- 텍스트 임베딩 추출, 임베딩 벡터 간 유사도 분석 기능 제공
- 실제 REST API 요청/응답 예제 및 인퍼런스 사용법 코드 포함
## 실행 및 환경 구성 예시
```bash
# Colab 환경 기준
!pip install sentence-transformers fastapi uvicorn pyngrok nest_asyncio

# 모델 로딩 샘플 (Python)
from sentence_transformers import SentenceTransformer
model = SentenceTransformer('Qwen/qwen3-embedding-0.6b')

# FastAPI 서버 실행 예 (Colab)
import nest_asyncio
nest_asyncio.apply()
from pyngrok import ngrok
public_url = ngrok.connect(8000)
```

## API 엔드포인트 예시

- **GET `/test`** :
  - 서버 동작 테스트용 기본 엔드포인트
  - 응답 예제: `{ "message": "Hello World" }`

- **POST `/embed`** :
  - 입력: `["문장1", "문장2", ...]` 형태의 리스트(JSON key: `inputs`)
  - 동작: 입력 문장들에 대한 임베딩 생성 및 해당 임베딩들 간 유사도 행렬 산출
  - 응답 예제:
    ```json
    {
      "embeddings": [
        [1.0, 0.93, ...],
        [0.93, 1.0, ...],
        ...
      ]
    }
    ```

## 원격 인퍼런스 & 데모
- 서버 구동 후 Colab URL 또는 pyngrok 주소로 외부 POST 테스트 가능(ngrok api key 필요)
- 실제 API 요청/응답 구조 및 코드 Colab 예제에 포함

## 참고 자료
- [Qwen3-Embedding-0.6B Colab 노트북(전체 코드/데모)](https://colab.research.google.com/drive/1jd2hDkavAH_F-w-2YX-EGvDgA56NoRJw)
- [FastAPI 공식 문서](https://fastapi.tiangolo.com/)
- [Qwen3 모델 공식 GitHub](https://github.com/QwenLM/Qwen3)
