# ACADEPOL — ID e telefone/código alfanuméricos

## Alterações
- ID da cidade aceita letras, números e hífen, até 32 caracteres.
- Telefone/código da cidade aceita letras, números e hífen, até 32 caracteres.
- A validação foi atualizada no cadastro público, edição de perfil e edição administrativa.
- ID/passaporte dos conscritos em recrutamentos também aceita letras, números e hífen.
- Campos deixaram de forçar teclado numérico e não removem mais letras.
- Valores numéricos de telefone com seis dígitos continuam sendo exibidos no formato `000-000`; valores alfanuméricos são exibidos como digitados.

## Banco de dados
As colunas `users.city_id`, `users.city_phone` e os campos de ID dos conscritos já são `TEXT`. Não é necessária migração nem alteração manual no Neon.

## Validação
- `node --check server.js`: aprovado.
- Sintaxe dos scripts inline de `public/index.html`: aprovada.

## Publicação
Substitua os arquivos pelo conteúdo deste pacote no GitHub, faça commit na branch `main` e aguarde o deploy do Render. Não altere as variáveis de ambiente nem recrie o banco Neon.
