# ACADEPOL — Redesign de identidade visual

Esta versão aplica uma direção visual própria para a ACADEPOL: Central de Formação, interface escura, vermelho como destaque e tons de branco/cinza para hierarquia visual.

## O que mudou
- Dashboard com hero institucional mais amplo e composição diferente.
- Faixa de indicadores com aparência editorial, sem o mosaico colorido antigo.
- Área principal em duas colunas: próximas atividades e resumo; ações rápidas em faixa própria.
- Menu e cabeçalho mais neutros, com marcador vermelho para seleção.
- Botões, indicadores, painéis e agenda harmonizados em preto, branco, cinza e vermelho.
- Rótulos do dashboard ajustados para linguagem de academia, mantendo IDs e integrações existentes.

## Publicação
1. Substitua os arquivos do repositório pelos arquivos deste pacote, preservando a estrutura `ACADEPOL/`.
2. Faça commit na branch `main`.
3. No Render, execute **Manual Deploy → Deploy latest commit**.
4. Após o deploy, use `Ctrl + F5` e teste login, navegação, agenda, ações rápidas e permissões.

## Importante
- Não altera `DATABASE_URL`, segredos ou o banco Neon.
- Mantém os IDs de interface usados pelos scripts existentes.
- A mudança é principalmente visual; os módulos e a lógica herdada ainda precisam ser reconstruídos separadamente para uma separação funcional completa do sistema anterior.
