# ACADEPOL — Academia de Polícia

Projeto com identidade visual própria em preto, branco, cinza e vermelho. A marca oficial ACADEPOL é usada no login e no painel; o hero cinematográfico fica restrito às áreas institucionais.

## Deploy
- Runtime: Node.js 20+
- Build: `npm install`
- Start: `npm start`
- Configure `DATABASE_URL`, `JWT_SECRET`, `ADMIN_USERNAME`, `ADMIN_PASSWORD` e `NODE_ENV=production` nas variáveis de ambiente do Render.
- Não versionar `.env` nem credenciais.

A atualização é visual e de textos de marca; preserva o backend e a lógica de negócio existentes. Faça deploy em ambiente de teste e valide login, módulos e conexão Neon após publicar.
