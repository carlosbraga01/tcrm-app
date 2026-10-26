# Deploy do TCRM — Railway e novos clientes

Arquitetura por instalação (um cliente = uma stack isolada):

| Serviço | O que é |
|---|---|
| `tcrm` | App Next.js (este repo, `Dockerfile` da raiz) |
| Supabase | Postgres + Auth + Realtime + Storage (projeto Supabase por cliente) |
| `waha` | `devlikeapro/waha:noweb` — WhatsApp HTTP API (opcional por cliente) |
| `worker` | `Dockerfile.worker` — drena o `event_log` (IA, follow-ups) |
| `scheduler` | `Dockerfile.scheduler` — crons internos |

## Variáveis essenciais (Railway → service `tcrm`)

```env
NEXT_PUBLIC_SUPABASE_URL=https://<projeto>.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=<anon key>
SUPABASE_SERVICE_ROLE_KEY=<service role key>
SUPABASE_SERVER_URL=https://<projeto>.supabase.co
INTERNAL_SECRET=<aleatório>
INTERNAL_CRON_SECRET=<aleatório>
TENANT_PROVISIONING_SECRET=<aleatório>

# Marca Telecom ME
APP_NAME=TCRM
APP_LOGO_URL=https://<dominio>/brand/tcrm-logo.png
APP_ACCENT_HEX=#2563EB
```

Os segredos `INTERNAL_*` são hex aleatórios de 32 bytes (`openssl rand -hex 32`).

## Passo a passo por cliente

1. **Supabase**: criar projeto em supabase.com (região mais próxima do cliente).
   Aplicar `supabase/baseline.sql` no SQL Editor (uma vez).
2. **Railway**: `New Project` → `Deploy from GitHub repo` → `carlosbraga01/tcrm-app`
   (Railway usa o `Dockerfile` da raiz automaticamente).
3. Adicionar os workers como serviços separados apontando para
   `Dockerfile.worker` e `Dockerfile.scheduler` (mesmas envs do app).
4. Gerar domínio público em Settings → Networking.
5. Ajustar `APP_LOGO_URL` para o domínio gerado (`https://<dominio>/brand/tcrm-logo.png`).
6. **WhatsApp (opcional)**: serviço WAHA (`devlikeapro/waha:noweb`) com volume;
   `WAHA_API_BASE_URL` apontando para ele + `WAHA_API_KEY`.
7. Login inicial: abrir `https://<dominio>/signup` e criar a conta do admin.

## Atualização

Push na `main` → Railway rebuilda e redeploya. Migrações de banco são
aplicadas pela tela ou manualmente via `supabase/migrations/` (o baseline cobre
instalações novas).

## Licença e atribuição

MIT: manter `LICENSE` e o aviso de copyright do DeskcommCRM. A marca própria do
cliente fica nas variáveis `APP_*` — nunca em patch de código (sobrevive a
updates da imagem).
