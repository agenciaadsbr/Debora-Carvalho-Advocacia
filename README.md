# Débora Carvalho Advocacia — LP Direito Previdenciário

Site estático (HTML/CSS/JS puro), mesmo padrão da LP Carlos Aiello (Vercel + Supabase "ADS BR CLIENTES").

## Rotas
| Rota | Arquivo | O que faz |
|---|---|---|
| `/` | `vercel.json` | redireciona para `/previdenciario` |
| `/previdenciario` | `previdenciario/index.html` | LP previdenciária com formulário (Nome + WhatsApp) |
| `/previdenciario/redirect` | `previdenciario/redirect.html` | rota exclusiva desta LP: agradece, espera 3 s e abre o WhatsApp |

## Leads (Supabase "ADS BR CLIENTES" · `qxhnjzyhtllmtdrcyygi`)
- Tabela `lp_leads` (já existente, sem migration): `site='debora-carvalho'`, `nome`, `whatsapp` (só dígitos), `origem` (google-ads / meta-ads / utm_source / domínio / direto), `servico` = `Direito Previdenciário` ou `Direito Previdenciário — <tema do card clicado>`.
- Visitas em `lp_visits` com `site='debora-carvalho'`.
- O redirect só acontece depois que o Supabase confirma a gravação (1 nova tentativa automática; se falhar, mostra erro e o visitante pode reenviar).

## Antes de publicar
1. **WhatsApp**: em `previdenciario/redirect.html`, preencher `WHATSAPP_NUMERO` (55 + DDD + número). Vazio = a página só agradece, sem redirecionar.
2. **Fotos**: hospedadas no bucket público `lp-assets/debora-carvalho/` do Supabase (originais em PNG) e servidas redimensionadas em WebP pelo endpoint `/storage/v1/render/image/` (hero 1600px, demais 1200px).
3. **Pixel / Google Ads**: há espaço reservado no `<head>` das duas páginas e no script do redirect para o evento de conversão.
4. **BPC/LOAS**: os blocos estão marcados com `data-servico="bpc"` (card, painel e link do rodapé) para remover fácil, se for o caso.

## Identidade
Tokens no topo do CSS (`.lp{--deep…}`): slate `#2F4147`/`#425961`, pêssego `#FDD1A1`, caramelo `#C9925A`, creme `#F5F0E8` — extraídos do logo e dos posts.
Logos em `assets/` (recortados do logo oficial, fundo transparente): `logo-claro.png`, `logo-escuro.png`, `logo-horizontal-claro.png`, `monograma.png`, `favicon.png`.
