# ACADEPOL — configuração inicial com Neon Free

O projeto usa PostgreSQL no Neon Free. Crie um projeto Neon exclusivo para ACADEPOL e configure `DATABASE_URL` no ambiente do serviço de hospedagem.

## Variáveis de ambiente
- `DATABASE_URL`: connection string PostgreSQL do Neon, com SSL.
- `JWT_SECRET`: segredo aleatório longo e exclusivo.
- `ADMIN_USERNAME`: usuário inicial de administração.
- `ADMIN_PASSWORD`: senha forte para a conta inicial.
- `NODE_ENV=production`.

O backend cria a estrutura de tabelas na inicialização. Use um banco novo, sem importar registros antigos. Nunca compartilhe a connection string ou publique o arquivo `.env`.

## Identidade visual
A interface foi retematizada com preto, branco e vermelho e usa apenas os novos recursos SVG `public/academia.svg` e `public/academia-bg.svg`; as imagens institucionais antigas foram removidas.
