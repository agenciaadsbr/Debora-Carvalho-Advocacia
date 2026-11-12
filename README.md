# Débora Carvalho Advocacia — LP Direito Previdenciário

Site estático (HTML/CSS/JS puro), mesmo padrão da LP Carlos Aiello (Vercel + Supabase "ADS BR CLIENTES").
Produção: https://debora-carvalho-advocacia.vercel.app — cada push na `main` publica automaticamente.

## Rotas
| Rota | Arquivo | O que faz |
|---|---|---|
| `/` | `vercel.json` | redireciona para `/previdenciario` |
| `/previdenciario` | `previdenciario/index.html` | LP previdenciária com formulário (Nome + WhatsApp) |
| `/previdenciario/redirect` | `previdenciario/redirect.html` | rota exclusiva desta LP: agradece, espera 3 s e abre o WhatsApp |
| `/dashboard` | `dashboard.html` | painel de leads com login (visitas, leads, conversão, lista com assunto e origem) |

## Conversão
- Todos os CTAs (verdes, com ícone do WhatsApp) levam ao formulário; o tema do card clicado vai junto no lead.
- O botão flutuante redondo do WhatsApp leva **direto** para `/previdenciario/redirect`, sem passar pelo formulário (esses cliques não viram lead no Supabase).

## Leads (Supabase "ADS BR CLIENTES" · `qxhnjzyhtllmtdrcyygi`)
- Tabela `lp_leads` (já existente, sem migration): `site='debora-carvalho'`, `nome`, `whatsapp` (só dígitos), `origem` (google-ads / meta-ads / utm_source / domínio / direto), `servico` = `Direito Previdenciário` ou `Direito Previdenciário — <tema do card clicado>`.
- Visitas em `lp_visits` com `site='debora-carvalho'`.
- O redirect só acontece depois que o Supabase confirma a gravação (1 nova tentativa automática; se falhar, mostra erro e o visitante pode reenviar).
- Dashboard: login `admin` → `admin@debora-carvalho.adsbr.internal` (Supabase Auth), liberado em `lp_acessos` com `site='debora-carvalho'`.

## Pendências
1. **WhatsApp**: em `previdenciario/redirect.html`, preencher `WHATSAPP_NUMERO` (55 + DDD + número). Vazio = a página só agradece, sem redirecionar.
2. **Login do dashboard**: criar o usuário no Supabase Auth e a linha em `lp_acessos`.
3. **Pixel / Google Ads**: há espaço reservado no `<head>` das duas páginas e no script do redirect para o evento de conversão.
4. **BPC/LOAS**: os blocos estão marcados com `data-servico="bpc"` (card, painel e link do rodapé) para remover fácil, se for o caso.

## Imagens
- Fotos da Dra. Débora (enviadas pela agência): `assets/dra-debora-hero.jpg` (topo) e `assets/dra-debora-sobre.jpg` (seção Sobre).
- Fotos das seções de benefícios: bucket público `lp-assets/debora-carvalho/` do Supabase (originais em PNG), servidas em WebP pelo endpoint `/storage/v1/render/image/` (1200px).

## Identidade
Tokens no topo do CSS (`.lp{--deep…}`): slate `#2F4147`/`#425961`, pêssego `#FDD1A1`, caramelo `#C9925A`, creme `#F5F0E8`, verde dos CTAs `#11823B` — extraídos do logo e dos posts.
Logos em `assets/` (recortados do logo oficial, fundo transparente): `logo-claro.png`, `logo-escuro.png`, `logo-horizontal-claro.png`, `monograma.png`, `favicon.png`.
