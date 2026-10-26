# Marca

## Símbolo e logotipo — TCRM · Telecom ME

| Arquivo | O que é |
|---|---|
| `tcrm-icon.png` | O símbolo "M" blocado da Telecom ME. |
| `tcrm-logo.png` | Logotipo horizontal para fundo claro — símbolo + "Telecom ME". |
| `tcrm-logo-on-dark.png` | Logotipo para fundo escuro. |

A tipografia oficial é a Inter; os tokens de cor vivem no design system da
Telecom ME (azul-noite `#0B1220`, azul `#2563EB`, ciano `#22D3EE`, grafite
`#111827`).

**Estes arquivos são a fonte da marca do produto; o app NÃO os lê.** Na
instalação, a marca vem das variáveis `APP_NAME`, `APP_LOGO_URL` e
`APP_ACCENT_HEX` (ver `lib/branding.ts`): o nome padrão do produto é `TCRM` e,
sem configuração, a interface cai na geometria desenhada em
`lib/branding/desenho.ts` — legado do produto de origem, substituída pela marca
da instalação assim que as variáveis acima são definidas.

Os logos de produção ficam em `public/brand/` para que `APP_LOGO_URL` possa
apontar para `/brand/tcrm-logo.png` no próprio domínio da instalação.

## Atribuição

TCRM é distribuído pela Telecom ME sobre a base open source DeskcommCRM
(licença MIT). O aviso de copyright e o arquivo `LICENSE` são mantidos conforme
a licença exige.
