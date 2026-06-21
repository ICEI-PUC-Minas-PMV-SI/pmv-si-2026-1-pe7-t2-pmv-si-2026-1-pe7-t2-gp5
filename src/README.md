# Cartão Churn

Código-fonte do projeto de previsão de churn: backend (Flask + XGBoost) e frontend (React + Vite). O dataset está em `src/backend/`.

---

**Pré-requisitos**: Python 3.10+, Node.js 18+.

Instalação (backend):

  cd src/backend
  python -m venv .venv
  .venv\Scripts\activate   (Windows)
  pip install -r requirements.txt
  python application.py

Observação: o treinamento do modelo é feito em background se o CSV estiver presente.

Exemplo (curl):

  curl -X POST http://localhost:5000/api/predict'
---

Instalação (frontend):

  cd src/frontend
  npm install
  npm run dev

O frontend assume a API em `http://localhost:5000`.
---
