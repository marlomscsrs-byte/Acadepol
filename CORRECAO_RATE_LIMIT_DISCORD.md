# Correção de rate limit do Discord

## Alterações
- Uma resposta HTTP 429 encerra imediatamente a chamada atual; não há repetição automática da mesma requisição.
- O `Retry-After` informado pelo Discord é respeitado como cooldown global local, com pequena margem de segurança.
- Chamadas novas durante o cooldown são recusadas localmente com resposta 429 sintética, sem tráfego adicional ao Discord.
- Requisições que já estavam na fila são canceladas localmente e recebem 429 sintético para evitar uma rajada quando o cooldown terminar.
- Logs de 429 registram `X-RateLimit-Scope`, `X-RateLimit-Global`, `X-RateLimit-Bucket` e a mensagem retornada, quando disponíveis.
- O limite de retries HTTP 429 foi desativado; chamadas de rede não devem contornar limites do Discord.

## Publicação
Substitua o projeto pelos arquivos deste pacote e faça deploy no Render. Não é necessário alterar variáveis de ambiente. Após o deploy, acompanhe os logs `[DISCORD API 429 DETALHE]`.

## Nota
Nenhum código pode garantir que o Discord nunca aplique rate limit, pois ele controla esses limites. Esta correção evita retries em rajada e chamadas acumuladas durante o cooldown. Operações adiadas podem precisar ser acionadas novamente por sua rotina ou fila após o limite liberar.
