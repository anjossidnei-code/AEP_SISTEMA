# 🏗️ AEP Sistema — Deploy no Vercel

Sistema de Geração de Laudos AEP NR-17 com autenticação de usuários.

## 📁 Estrutura de Arquivos

```
aep-web/
├── index.html          ← Tela de login
├── sistema.html        ← Gerador de laudo (usuários logados)
├── vercel.json         ← Configuração do Vercel
├── .gitignore
├── admin/
│   └── index.html      ← Painel administrativo
└── data/
    └── config.js       ← ⚠️ Usuários e empresas (MANTENHA O REPO PRIVADO)
```

---

## 🚀 Passo a Passo: Deploy no Vercel

### 1. Criar repositório no GitHub (PRIVADO)

1. Acesse [github.com](https://github.com) → **New repository**
2. Nome: `aep-sistema` (ou qualquer nome)
3. **⚠️ Selecione PRIVATE** (não Public — o config.js tem hashes de senha)
4. Clique em **Create repository**

### 2. Enviar os arquivos

No terminal (ou Git Bash no Windows):

```bash
cd /caminho/para/aep-web
git init
git add .
git commit -m "Initial deploy AEP Sistema"
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/aep-sistema.git
git push -u origin main
```

### 3. Conectar ao Vercel

1. Acesse [vercel.com](https://vercel.com) e faça login com GitHub
2. Clique em **Add New Project**
3. Selecione o repositório `aep-sistema`
4. Clique em **Deploy** (sem alterar nada)
5. Aguarde ~30 segundos
6. Seu sistema estará em: `https://aep-sistema-SEU_USUARIO.vercel.app`

---

## 👤 Primeiro acesso

**Login padrão:**
- Usuário: `admin`
- Senha: `admin123`

**⚠️ Troque a senha imediatamente:**
1. Acesse `/admin`
2. Aba **Gerar Hash de Senha** → gere o hash da nova senha
3. Aba **Usuários** → edite o admin com o novo hash
4. Aba **Gerar config.js** → baixe o novo config.js
5. Substitua `data/config.js` no repositório
6. `git add . && git commit -m "update admin password" && git push`

---

## ➕ Adicionar usuário

1. Acesse `/admin`
2. Aba **Usuários** → **+ Novo Usuário**
3. Preencha login, nome, senha
4. Selecione a empresa que o usuário pode acessar
5. Salve → Gere o config.js → Baixe → Substitua no GitHub → git push

---

## 🏢 Adicionar empresa

1. Acesse `/admin`
2. Aba **Empresas** → **+ Nova Empresa**
3. Preencha nome, CNPJ
4. Importe o **logo** (PNG/JPG)
5. Adicione os **responsáveis técnicos** com assinaturas
6. Salve → Gere o config.js → Baixe → Substitua no GitHub → git push

---

## 🔄 Atualizar após mudanças

Sempre que alterar usuários, empresas, logo ou assinaturas:

```bash
# Substitua o data/config.js pelo arquivo baixado do painel admin
cp ~/Downloads/config.js data/config.js

git add data/config.js
git commit -m "update config"
git push
```

O Vercel faz o deploy automático em ~30 segundos.

---

## 🔑 Segurança

- O repositório **DEVE ser privado** no GitHub
- As senhas são armazenadas como **hash SHA-256** (não reversível)
- As sessões expiram em **8 horas** automaticamente
- Usuários inativos (`ativo: false`) não conseguem logar

---

## 📞 Fluxo do usuário

```
Usuário acessa a URL → Login → Sistema AEP carrega
  → Logo e responsáveis da empresa são pré-carregados automaticamente
  → Usuário importa a planilha .xlsx
  → Gera o laudo com todos os dados
  → Salva como PDF
```
