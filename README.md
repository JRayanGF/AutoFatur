# Gerador de Relação de Faturamento

Sistema web para geração automática de relatórios de faturamento com integração Supabase e deploy no Netlify.

---

## 🗄️ 1. Configurar o Supabase

1. Acesse [supabase.com](https://supabase.com) e crie um projeto
2. No painel, vá em **SQL Editor** e execute:

```sql
create table relatorios (
  id uuid default gen_random_uuid() primary key,
  empresa text not null,
  cnpj text,
  regime text,
  socio text,
  data_inicio text,
  data_fim text,
  valor_medio numeric,
  faturamentos jsonb,
  criado_em timestamptz default now()
);

-- Permitir acesso público (ajuste conforme necessário)
alter table relatorios enable row level security;
create policy "Allow all" on relatorios for all using (true) with check (true);
```

3. Vá em **Settings > API** e copie:
   - **Project URL** → `VITE_SUPABASE_URL`
   - **anon public key** → `VITE_SUPABASE_ANON_KEY`

---

## 💻 2. Rodar localmente

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/relatorio-faturamento.git
cd relatorio-faturamento

# Instale as dependências
npm install

# Crie o arquivo de variáveis de ambiente
cp .env.example .env
# Edite o .env com suas chaves do Supabase

# Inicie o servidor de desenvolvimento
npm run dev
```

---

## 🚀 3. Deploy no Netlify via GitHub

1. Faça push do projeto para um repositório no GitHub:
```bash
git init
git add .
git commit -m "primeiro commit"
git remote add origin https://github.com/seu-usuario/relatorio-faturamento.git
git push -u origin main
```

2. Acesse [netlify.com](https://netlify.com) → **Add new site** → **Import from Git**
3. Selecione seu repositório
4. As configurações de build já estão no `netlify.toml`:
   - **Build command:** `npm run build`
   - **Publish directory:** `dist`
5. Vá em **Site settings > Environment variables** e adicione:
   - `VITE_SUPABASE_URL` = sua URL do Supabase
   - `VITE_SUPABASE_ANON_KEY` = sua chave anon do Supabase
6. Clique em **Deploy site** ✅

A partir daí, todo `git push` faz deploy automático!

---

## ✨ Funcionalidades

- Gerar faturamentos fictícios por período com variação configurável
- Pré-visualização fiel ao documento Word original
- Assinar digitalmente com assinatura do Daniel Dager
- Baixar PDF com layout idêntico ao modelo
- Salvar relatórios no Supabase
- Histórico completo com edição e exclusão
