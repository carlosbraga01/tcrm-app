<p align="center">
  <img src="docs/brand/tcrm-logo.png" alt="TCRM — Telecom ME" width="420">
</p>

<h1 align="center">TCRM</h1>

<p align="center">
  CRM de vendas com agentes de IA e WhatsApp nativo — o produto da Telecom ME
  para operação comercial multi-tenant, self-hosted e pronto para LGPD.
</p>

---

## O que é

O **TCRM** é o CRM da **Telecom ME**: um sistema operacional de vendas
self-hosted que reúne pipeline, inbox de WhatsApp, agentes de IA e automações
num só produto. Ele é distribuído por instalação — cada cliente roda a própria
instância com a própria marca, banco e credenciais.

Baseado no projeto open source **DeskcommCRM** (licença MIT), mantido aqui com
o aviso de copyright e o `LICENSE` originais.

## Stack

Next.js 16 (App Router) · React 19 · TypeScript estrito · Tailwind 4 ·
Supabase (Postgres + Auth + Realtime + Storage) · WAHA (WhatsApp) ·
Vercel AI Gateway · Upstash Redis.

## Marca por instalação (white-label)

A marca de cada instalação é configurada por variáveis de ambiente, sem rebuild:

```env
APP_NAME=TCRM
APP_LOGO_URL=https://seu-dominio/brand/tcrm-logo.png
APP_ACCENT_HEX=#2563EB
```

- `APP_NAME` — nome exibido na interface, títulos e e-mails.
- `APP_LOGO_URL` — URL pública do logotipo (os assets da Telecom ME ficam em
  `public/brand/`).
- `APP_ACCENT_HEX` — cor-semente da marca; dela sai a rampa de 11 tons que pinta
  todo o produto nos dois temas.

## Deploy

Ver [`docs/DEPLOY-TCRM.md`](docs/DEPLOY-TCRM.md) — implantação no Railway
(app + Supabase + WAHA) e checklist para novos clientes.

## Guias embutidos do assistente

O repositório traz **guias do assistente** em `.agents/skills/` (instalar,
montar cliente por nicho, métricas, prompt do agente, contribuir), carregados
sozinhos pelo Claude Code, Codex, Cursor, OpenCode ou Antigravity. Para tê-los
em **qualquer pasta**, rode uma vez:

```bash
curl -fsSL https://raw.githubusercontent.com/carlosbraga01/tcrm-app/main/scripts/instalar-guias.sh | bash
```

Para chamar um guia pelo nome: `/deskcomm-instalar` no Claude Code, no Cursor
e no Antigravity; `$deskcomm-instalar` no Codex; no OpenCode, pelo nome em
linguagem natural.

Os guias **não** se atualizam sozinhos: rodar o mesmo comando de novo traz a
versão nova. Com o repositório clonado eles já vêm dentro dele; se você rodou o
comando mesmo assim, no Claude Code o guia instalado vale mais que o do clone —
fica na versão do dia em que rodou, até rodar de novo — ou desfazer:

```bash
curl -fsSL https://raw.githubusercontent.com/carlosbraga01/tcrm-app/main/scripts/instalar-guias.sh | bash -s -- --remover
```

## Licença

MIT — ver `LICENSE`. A atribuição do DeskcommCRM é preservada conforme exige a
licença.
