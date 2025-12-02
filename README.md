# novel-ragger

Small project that loads documents, builds embeddings and stores vectors for retrieval. Intended for local experimentation with LangChain, ChromaDB and document loaders.

## Requirements

- Python 3.11 (recommended). Many pinned packages in requirements.txt declare an upper Python bound and will not install on Python 3.14.
- Windows (commands below use PowerShell).
- Microsoft Visual C++ Build Tools (if you need to install onnxruntime for chromadb).

## Quick setup (Windows PowerShell)

1. Install Python 3.11 (if not installed):
```powershell
winget install --id=Python.Python.3.11 -e
```

2. Recreate a clean virtual environment and install dependencies:
```powershell
# from project root
Remove-Item -Recurse -Force .\.venv
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r .\requirements.txt
```

If pip fails on a specific pinned package (for example `unstructured==0.14.4`), either:
- Update requirements.txt to use an available compatible version (example: `unstructured==0.18.21`), or
- Use the Python version the pinned packages expect (3.11 is safest).

## Common problems & fixes

- "Fatal error in launcher: Unable to create process ..."  
  Cause: pip/launcher scripts in the venv reference a different project's Python executable.  
  Fix: delete and recreate the venv (commands above) so scripts point to the correct Python.

- "No matching distribution found for unstructured==0.14.4"  
  Cause: that exact version is not available on PyPI or not compatible with your Python version.  
  Fix: pick a published version (see pip error list) and update requirements.txt.

## Usage

1. Activate the venv:
```powershell
.\.venv\Scripts\Activate.ps1
```
2. Run the project's main script (replace `main.py` with the real entrypoint if different):
```powershell
python main.py
```

## Development notes

- Use VS Code Python extension. Ensure the workspace interpreter is set to `.venv\Scripts\python.exe`.
- If you add markdown processing, install `unstructured[md]` after base deps:
```powershell
pip install "unstructured[md]"
```

## Contributing

Create issues / PRs. Keep dependency pins compatible with Python 3.11 for CI reproducibility.

## License

Specify your license here.

## Dependencies tree 

Your Project
├── python-dotenv==1.0.1
├── langchain==0.2.2
├── langchain-community==0.2.3
├── langchain-openai==0.1.8
├── unstructured==0.14.4
├── chromadb==0.5.0
├── openai==1.31.1
└── tiktoken==0.7.0


langchain==0.2.2
├── langchain-core==0.2.43
│   ├── pydantic==2.12.5
│   │   ├── annotated-types==0.7.0
│   │   ├── pydantic-core==2.41.5
│   │   └── typing-extensions==4.15.0
│   ├── SQLAlchemy==2.0.44
│   │   └── greenlet==3.2.4
│   ├── tenacity==8.5.0
│   └── jsonpatch==1.33
│       └── jsonpointer==3.0.0
├── langchain-text-splitters==0.2.4
├── langsmith==0.1.147
│   ├── requests==2.32.5
│   │   ├── certifi==2025.11.12
│   │   ├── charset-normalizer==3.4.4
│   │   ├── idna==3.11
│   │   └── urllib3==2.3.0
│   ├── orjson==3.11.4
│   └── dataclasses-json==0.6.7
│       └── marshmallow==3.26.1
└── PyYAML==6.0.3


chromadb==0.5.0
├── fastapi==0.123.4
│   ├── starlette==0.50.0
│   │   ├── anyio==4.12.0
│   │   │   └── idna==3.11
│   │   │   └── sniffio==1.3.1
│   │   └── typing-extensions==4.15.0
│   ├── pydantic==2.12.5 (already installed)
│   └── python-multipart (not installed for you)
├── uvicorn==0.38.0
│   ├── click==8.3.1
│   ├── h11==0.16.0
│   ├── httptools==0.7.1
│   ├── python-dotenv==1.0.1 (already from you)
│   ├── uvloop (not on Windows)
│   └── watchfiles==1.1.1
├── onnxruntime==1.23.2
│   ├── numpy==1.26.4
│   ├── sympy==1.14.0
│   │   ├── mpmath==1.3.0
│   │   └── typing-extensions==4.15.0
│   └── flatbuffers==25.9.23
├── grpcio==1.76.0
│   ├── six==1.17.0
│   └── setuptools==65.5.0
├── chroma-hnswlib==0.7.3
├── posthog==7.0.1
├── bcrypt==5.0.0
│   └── cffi==2.0.0
│       └── pycparser==2.23
├── kubernetes==34.1.0
│   ├── google-auth==2.43.0
│   │   ├── cachetools==6.2.2
│   │   ├── pyasn1==0.6.1
│   │   ├── pyasn1-modules==0.4.2
│   │   ├── rsa==4.9.1
│   │   └── six==1.17.0
│   ├── oauthlib==3.3.1
│   ├── requests-oauthlib==2.0.0
│   │   ├── oauthlib==3.3.1
│   │   └── requests==2.32.5
│   ├── googleapis-common-protos==1.72.0
│   └── urllib3==2.3.0
├── mmh3==5.2.0
├── overrides==7.7.0
├── opentelemetry-api==1.38.0
│   ├── typing-extensions==4.15.0
│   └── opentelemetry-semantic-conventions==0.59b0
├── opentelemetry-sdk==1.38.0
│   ├── opentelemetry-api==1.38.0 (already)
│   └── opentelemetry-exporter-otlp-proto-grpc==1.38.0
│       ├── opentelemetry-exporter-otlp-proto-common==1.38.0
│       │   ├── opentelemetry-proto==1.38.0
│       │   └── protobuf==6.33.1
│       └── googleapis-common-protos==1.72.0
├── opentelemetry-instrumentation-fastapi==0.59b0
│   ├── opentelemetry-instrumentation-asgi==0.59b0
│   │   ├── opentelemetry-instrumentation==0.59b0
│   │   │   └── opentelemetry-api==1.38.0
│   │   └── opentelemetry-util-http==0.59b0
│   └── wrapt==1.17.3
└── PyPika==0.48.9


unstructured==0.14.4
├── lxml==6.0.2
├── python-magic==0.4.27
├── unstructured-client==0.42.4
│   ├── requests==2.32.5 (already)
│   ├── typing-extensions==4.15.0 (already)
│   └── filetype==1.2.0
├── pypdf==6.4.0
├── nltk==3.9.2
│   ├── click==8.3.1 (already)
│   ├── joblib==1.5.2
│   └── tqdm==4.67.1
├── beautifulsoup4==4.14.3
│   └── soupsieve==2.8
├── langdetect==1.0.9
├── markdown-it-py==4.0.0
│   ├── mdurl==0.1.2
│   └── typing-extensions==4.15.0 (already)
├── huggingface-hub==1.1.7
│   ├── filelock==3.20.0
│   ├── fsspec==2025.10.0
│   ├── packaging==24.2
│   ├── pyyaml==6.0.3 (already)
│   ├── requests==2.32.5 (already)
│   ├── tqdm==4.67.1 (already)
│   └── typing-extensions==4.15.0 (already)
└── python-iso639==2025.11.16


openai==1.31.1
├── anyio==4.12.0 (already)
├── distro==1.9.0
├── httpx==0.28.1
│   ├── httpcore==1.0.9
│   │   ├── h11==0.16.0 (already)
│   │   └── typing-extensions==4.15.0 (already)
│   ├── certifi==2025.11.12 (already)
│   └── idna==3.11 (already)
├── pydantic==2.12.5 (already)
├── sniffio==1.3.1 (already)
└── typing-extensions==4.15.0 (already)