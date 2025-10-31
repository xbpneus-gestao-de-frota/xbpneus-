# XBPNEUS — Gestão de Frotas focada em Pneus

Este repositório contém o **sistema completo** (backend Django + frontend + gateway) e a **infra mínima** para rodar local e preparar deploy **sem executar o deploy agora**.

## Estrutura
- `backend/` – API Django (DRF, JWT, CORS, healthcheck)
- `frontend/` – App React/Vite (UI operacional)
- `gateway/` – FastAPI como API Gateway opcional
- `infra/` – DevOps: Docker Compose, Render, GitHub Actions
- `e2e/` – Testes Playwright
- `data/` – Catálogos de pneus/veículos/posições

## Como rodar local (Docker Compose)
```bash
docker compose up --build
# Backend: http://localhost:8000/api
# Frontend: http://localhost:5173
```

> **Importante:** Este commit deixa o repositório **pronto para deploy** no Render/K8s, mas **não aciona deploy**.

## Deploy (preparado, porém não executado)
- Render: arquivo `render.yaml` com serviços (backend/frontend/redis/db).
- GitHub Actions: `ci.yml` apenas **builda** as imagens e valida o projeto (sem `kubectl apply` e sem publicar Docker).

## Comandos úteis
```bash
# Backend: migrações
python manage.py makemigrations && python manage.py migrate

# Superusuário rápido (temporário; use secrets no Render)
python manage.py createsuperuser
```

## Segurança
- Segredos via variáveis de ambiente (nunca commitar credenciais).
- `DEBUG=False` em produção.
- CORS/CSRF já configurados nas settings de produção.
