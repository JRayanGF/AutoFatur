# Gerador de Relação de Faturamento — Dager Hub

---

## ✅ Credenciais já configuradas

O projeto já está configurado com o Supabase correto:
- **URL:** https://kxptcjbweunmodxdxhjf.supabase.co

---

## 🗄️ PASSO 1 — Criar a tabela no Supabase

1. Acesse: https://supabase.com/dashboard/project/kxptcjbweunmodxdxhjf
2. No menu lateral, clique em **SQL Editor**
3. Cole e execute o SQL abaixo:

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

alter table relatorios enable row level security;
create policy "Allow all" on relatorios for all using (true) with check (true);
```

4. Clique em **Run** ✅

---

## 💻 PASSO 2 — Subir no GitHub

```bash
# Extraia o zip e entre na pasta
cd relatorio-faturamento

# Instale as dependências
npm install

# Teste local (opcional)
npm run dev

# Suba para o GitHub
git init
git add .
git commit -m "init"
git remote add origin https://github.com/SEU-USUARIO/relatorio-faturamento.git
git push -u origin main
```

---

## 🚀 PASSO 3 — Deploy no Netlify

1. Acesse [netlify.com](https://app.netlify.com)
2. Clique em **Add new site → Import from Git**
3. Selecione o repositório que você subiu no GitHub
4. As configurações de build já estão prontas no `netlify.toml`
5. **NÃO precisa configurar variáveis de ambiente** — já estão no código
6. Clique em **Deploy site** ✅

Pronto! Todo `git push` fará deploy automático.

---

## ✨ Funcionalidades

- Gerar faturamentos fictícios por período com variação configurável
- Pré-visualização fiel ao documento original com logo e fundo
- Assinar digitalmente com assinatura do Daniel Dager
- Baixar PDF com layout idêntico ao modelo Word
- 💾 Salvar relatórios no Supabase
- 📋 Histórico com edição e exclusão
