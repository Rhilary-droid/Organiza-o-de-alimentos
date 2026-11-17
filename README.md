# Merenda Escolar — Jardim Cumbica II

Aplicação web responsiva para controle de estoque de alimentos, entradas, saídas, validade, histórico e exportação CSV. Backend PostgreSQL e autenticação no Supabase.

## Serviços
- Supabase: projeto `merenda-jardim-cumbica-ii`
- GitHub Pages: publicação estática por GitHub Actions
- URL do banco: `https://qdgfyhkxvhlneaiwkwxn.supabase.co`
- A chave publishable está no cliente; nunca inserir service_role/secret no navegador.

## Publicação
1. No GitHub, abra Settings → Pages.
2. Em Build and deployment, selecione **GitHub Actions** como Source.
3. O workflow `.github/workflows/pages.yml` publica automaticamente a cada push em `main`.
4. O endereço esperado do site é `https://rhilary-droid.github.io/Organiza-o-de-alimentos/`.

## Primeiro administrador
1. No Supabase → Authentication → Users → Add user, crie a conta administrativa.
2. No SQL Editor, execute substituindo pelo UUID real:
   ```sql
   update public.profiles
   set role = 'admin', full_name = 'Administrador'
   where id = 'UUID-REAL-DA-CONTA';
   ```
3. Confirme que a consulta afetou uma linha e entre no site.
4. Crie os demais usuários pelo painel Authentication. Eles recebem perfil `cozinheira` automaticamente.

## Papéis
- admin: consulta, cadastra e edita produtos; registra entradas e saídas.
- cozinheira: consulta estoque e registra entradas e saídas.
- Histórico de movimentações é somente leitura no aplicativo; alteração do saldo por movimentação usa função SQL transacional.

## Segurança e operação
- RLS está habilitado nas tabelas.
- Criar um login individual por pessoa; não compartilhar senhas.
- Não cadastrar dados pessoais de alunos.
- Testar primeiro com produtos fictícios e validar com a gestão da escola/rede antes do uso oficial.
- Câmera/leitura de código de barras e operações exigem navegador compatível e HTTPS.
- O plano gratuito tem limites, incluindo pausa por inatividade; manter exportações/backups conforme as regras da rede.
