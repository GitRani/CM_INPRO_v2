# CM_INPRO_v2

CM V2 Version Migration을 위한 대규모 Structure Work

CM_INPRO_V2/
├── app/                                # 메인 FastAPI 애플리케이션 디렉토리
│   ├── __init__.py                     # Python 패키지 초기화 파일
│   ├── app.py                          # FastAPI 앱의 메인 엔트리 포인트. 미들웨어, 라우터, 예외 핸들러 등을 설정
│   ├── common/                         # 여러 모듈에서 공통으로 사용되는 유틸리티 디렉토리
│   │   ├── __init__.py
│   │   ├── logging/                    # 로깅 설정을 담당하는 디렉토리
│   │   └── redis/                      # Redis 연결 및 관련 유틸리티를 관리하는 디렉토리
│   ├── config/                         # 애플리케이션 설정 디렉토리
│   │   └── config.py                   # 환경 변수 로드 및 애플리케이션의 주요 설정을 관리
│   ├── core/                           # 애플리케이션의 핵심 로직 디렉토리
│   │   ├── database.py                 # 데이터베이스 세션 생성 및 관리를 담당
│   │   └── dependencies.py             # FastAPI의 의존성 주입(Dependency Injection) 관련 로직 (예: 사용자 인증)
│   ├── docs/                           # 문서, 데이터, 업로드된 파일 등을 저장하는 디렉토리
│   │   ├── data/
│   │   ├── result/
│   │   ├── uploadfiles/
│   │   └── uploads/
│   ├── modules/                        # 주요 비즈니스 로직을 포함하는 모듈 디렉토리
│   │   ├── chat/                       # 챗봇 데이터 관리 관련 비즈니스 로직
│   │   │   ├── __init__.py
│   │   │   ├── answer_evaluator.py     # 챗봇 답변의 정오답을 평가하는 로직
│   │   │   ├── answer_sheet_manager.py # 정오답 체크용 정답지를 관리하는 로직
│   │   │   ├── data_transformer.py     # 운영 데이터를 분석 가능한 형태로 변환하는 로직
│   │   │   ├── dictionary_generator.py # 도메인 사전을 생성/관리하는 로직
│   │   │   └── learning_data_generator.py # Q&A 데이터를 기반으로 학습 데이터를 생성하는 로직
│   │   └── rag/                        # RAG 파이프라인 관련 비즈니스 로직
│   │       ├── function/
│   │       │   ├── agent/
│   │       │   │   └── rag_agent.py    # RAG 에이전트 및 그래프를 정의하는 로직
│   │       │   ├── document_processing/
│   │       │   │   ├── __init__.py
│   │       │   │   ├── chunker_de.py # Document Intelligence를 사용한 문서 청킹 로직
│   │       │   │   ├── chunker_di.py # Document Intelligence를 사용한 다른 방식의 청킹 로직
│   │       │   │   └── chunker.py    # 일반 문서 청킹 로직
│   │       │   ├── generate_query/
│   │       │   │   ├── concatenate_bpmn_pdf.py # BPMN과 PDF를 합치는 유틸리티
│   │       │   │   ├── generation_query.py     # 질문 생성의 메인 로직
│   │       │   │   ├── processing_bpmn.py      # BPMN 파일 처리 로직
│   │       │   │   ├── processing_pdf.py       # PDF 파일 처리 로직
│   │       │   │   └── prompt/
│   │       │   │       └── generate_question_prompt.yaml # 질문 생성을 위한 프롬프트
│   │       │   └── vector_store/
│   │       │       ├── clear_collection.py # Vector DB 컬렉션을 삭제하는 로직
│   │       │       └── embedding.py        # 텍스트를 임베딩하여 Vector DB에 저장하는 로직
│   │       ├── models/
│   │       │   └── yolov10x_best.pt        # YOLO 모델 가중치 파일
│   │       └── utils/
│   │           ├── extract_settings.py     # 설정 추출 유틸리티
│   │           ....
│   │ 
│   ├── routers/                        # API 엔드포인트를 정의하는 라우터 디렉토리
│   │   ├── auth/                       # 인증 및 사용자 관리 관련 API 라우터
│   │   │   └── views.py                # 인증/사용자 관련 웹 페이지를 렌더링하고 API를 처리
│   │   ├── chat/                       # 챗봇 데이터 관리 관련 API 라우터
│   │   │   ├── downloads.py            # 생성된 파일 다운로드 관련 API
│   │   │   ├── uploads.py              # 파일 업로드 및 처리 시작 관련 API
│   │   │   └── views.py                # 챗봇 관리 기능의 웹 페이지를 렌더링
│   │   ├── rag/                        # RAG 파이프라인 관련 API 라우터
│   │   │   ├── collections.py          # Vector DB 컬렉션 관리 API
│   │   │   ├── core.py                 # RAG 핵심 기능(채팅, 일괄처리) API
│   │   │   ├── tasks.py                # 백그라운드 작업 상태 조회/취소 API
│   │   │   └── views.py                # RAG 기능 관련 웹 페이지를 렌더링
│   │   └── utils.py                    # 여러 라우터에서 공용으로 사용하는 API (상태 체크, 로그 조회 등)
│   ├── schema/                         # Pydantic 스키마(데이터 모델) 디렉토리
│   │   ├── __init__.py
│   │   ├── rag.py                      # RAG 관련 데이터 모델 정의
│   │   └── user.py                     # 사용자 관련 데이터 모델 정의
│   ├── static/                         # 정적 파일(CSS, JavaScript, 이미지 등) 디렉토리
│   │   ├── css/
│   │   ├── js/
│   │   ├── images/
│   │   └── fonts/
│   └── templates/                      # Jinja2 HTML 템플릿 디렉토리
│       ├── auth/                       # 인증 관련 HTML 템플릿
│       │   ├── basic.html              # 기본 랜딩 페이지
│       │   ├── login.html              # 로그인 페이지
│       │   └── signup.html             # 회원가입 페이지
│       ├── chat/                       # 챗봇 관리 페이지 관련 HTML 템플릿
│       │   ├── answer-check.html       # 정오답 체크 페이지
│       │   ├── data-transform.html     # 운영 데이터 변환 페이지
│       │   ├── dictionary-data.html    # 사전 데이터 관리 페이지
│       │   ├── file-management.html    # 파일 관리 및 다운로드 페이지
│       │   └── learning-data.html      # 학습 데이터 생성 페이지
│       ├── etc/                        # 기타 페이지 HTML 템플릿
│       │   ├── laboratory.html         # 기능 실험실 페이지
│       │   └── redis-log-check.html    # Redis 로그 조회 페이지
│       ├── rag/                        # RAG 기능 관련 HTML 템플릿
│       │   ├── attu.html               # Milvus UI(Attu)를 임베드하는 페이지
│       │   ├── document-chunking.html  # 문서 청킹 및 임베딩 페이지
│       │   ├── excel_rag_generator.html # Excel 기반 RAG 답변 생성 페이지
│       │   ├── pdf_question_generator.html # PDF 기반 질문 생성 페이지
│       │   └── rag_chat.html           # RAG 채팅 테스트 페이지
│       └── shared/                     # 여러 템플릿에서 공통으로 사용하는 부분
│           ├── admin.html              # 관리자용 사용자 승인 페이지
│           └── layout.html             # 전체 페이지의 기본 레이아웃(헤더, 푸터, 네비게이션 포함)
├── front/                              # 프론트엔드 소스 코드 디렉토리 (Node.js)
│   ├── package.json                    # Node.js 프로젝트의 의존성 및 스크립트 정의
│   └── package-lock.json               # 의존성의 정확한 버전을 관리
├── logs/                               # 애플리케이션 로그 파일 저장 디렉토리
├── test/                               # 테스트 코드 및 샘플 디렉토리
│   ├── check_answer_backup.py
│   ├── env_test.py
│   ├── restart.py
│   ├── chat_sample/
│   └── rag_sample/
├── volumes/                            # Docker 볼륨 데이터 저장 디렉토리 (DB, Redis 등)
│   ├── mysql-data/
│   └── redis-data/
├── .gitignore                          # Git에서 추적하지 않을 파일 및 디렉토리 목록
├── docker-compose.yml                  # Docker Compose를 이용한 다중 컨테이너 서비스 정의 파일
├── Dockerfile                          # FastAPI 애플리케이션의 Docker 이미지 빌드를 위한 설정 파일
├── nginx.conf                          # Nginx 리버스 프록시 서버 설정 파일
├── README.md                           # 프로젝트 설명 파일
└── requirements.txt                    # Python 프로젝트의 의존성 패키지 목록
