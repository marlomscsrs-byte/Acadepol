# Otimização de tráfego — Instrutores Sistema

Esta versão inclui mudanças para reduzir transferências repetidas sem remover telas ou recursos:

- Respostas JSON maiores que 1 KB são comprimidas com Gzip quando o navegador aceita.
- `/api/bookings` retorna apenas colunas necessárias e não inclui fotos de perfil.
- `/api/instruction-uniforms` só retorna `image_data` quando a chamada usa `?images=1`.
- `/api/users` e `/api/recruitments/recruiters` omitem imagens Base64 por padrão; `?avatars=1` é usado apenas na tela de instrutores que exibe fotos.
- `/api/weekly-activity` e `/api/recognition` não retransmitem fotos em seus conjuntos de dados; as telas usam iniciais, preservando ranking, métricas e detalhes.
- O cliente compartilha chamadas GET simultâneas e mantém cache curto para `/api/bookings` e `/api/users`, e cache de 5 minutos para uniformes com imagens.
- Escritas via API invalidam o cache local.
- O ciclo de atualização geral não se sobrepõe e passou para 120 segundos; fica pausado em abas ocultas.
- A presença mantém as fotos fora da atualização periódica e só as carrega ao abrir o painel.

## Implantação segura

1. Faça backup/export do banco de dados antes de publicar.
2. Publique o conteúdo deste projeto no ambiente de teste ou como deploy do Render.
3. Mantenha as variáveis de ambiente e o banco de dados existentes.
4. Teste login, agenda, dashboard, edição/criação de marcações, relatórios, presença, uniformes, aprovações e recrutamentos.
5. No DevTools > Network, confira em `/api/bookings` o `Content-Encoding: gzip` e compare a coluna transferida após recarregar. O corpo descomprimido pode continuar grande em `Resource size`, mas o tráfego efetivo deve diminuir.

A compressão reduz os bytes transferidos; o cache reduz requisições repetidas durante janelas curtas. A economia real depende do tamanho dos dados e deve ser confirmada no Render após a publicação.
- A aba Materiais de Apoio carrega agora os comandos dos uniformes sem imagens; as imagens grandes são solicitadas somente quando a aba Uniformes é aberta. O editor continua buscando as imagens quando necessário.


## V5 — otimização geral de abas (2026-10-09)
- Cache GET privado em memória com TTLs curtos por endpoint e invalidação após mutações.
- Deduplicação de requisições GET simultâneas, inclusive para endpoints sem cache.
- Heartbeat não limpa o cache inteiro a cada minuto.
- Polling de notificações e pendências pausado quando a página está oculta; heartbeat mantido para preservar presença online.
- Atualização dos dados visíveis ao retornar à aba.
- Corrigido bloqueio do atualizador geral quando ele encontra um formulário/modal aberto.
- `public/index.html.gz` regenerado a partir do HTML final.


## V7 — intervalos de consulta
- Atualização geral da área ativa: a cada 20 minutos.
- Notificações: a cada 20 minutos.
- Usuários e marcações pendentes: a cada 20 minutos.
- Lista de presença: a cada 20 minutos.
- Heartbeat de presença mantido a cada 60 segundos para preservar o status online.
- Ações manuais e carregamento ao abrir telas continuam podendo consultar dados imediatamente.


## V8 — atualização de indicadores ao meio-dia
- Indicadores automáticos do Dashboard, Relatórios e Capacitação atualizam uma vez por dia às 12:00, no horário local do navegador.
- O ciclo geral de dados operacionais permanece a cada 20 minutos, exceto telas de indicadores consolidados.
- Ao retornar para a aba do navegador, dispara-se apenas o heartbeat; não há atualização automática imediata de todas as consultas.
- A abertura manual de uma tela continua carregando seus dados para evitar exibir informações vazias.
- Heartbeat de presença continua a cada 60 segundos; lista de presença, notificações e pendências mantêm seus intervalos próprios de 20 minutos.


## V9 — heartbeat sem duplicação
- Heartbeat periódico alterado para 5 minutos.
- Um único temporizador de presença por sessão; startPresence é idempotente.
- Um único listener de visibilitychange, com proteção contra chamadas duplicadas em menos de 30 segundos.
- Ao voltar à aba, tenta atualizar a presença imediatamente, respeitando a proteção anti-rajada.
- Expiração visual de presença ajustada para 10 minutos no endpoint /api/presence, para tolerar atrasos sem marcar usuários ativos como offline.
