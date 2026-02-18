# ✅ TADA-List

> **Feito pra ser concluído.** Um gerenciador de tarefas moderno com sincronização na nuvem via Firebase.

![HTML](https://img.shields.io/badge/HTML-single%20file-f5c842?style=flat-square)
![Firebase](https://img.shields.io/badge/Firebase-Firestore%20%2B%20Auth-ff6b35?style=flat-square&logo=firebase)
![GitHub Pages](https://img.shields.io/badge/deploy-GitHub%20Pages-4ade80?style=flat-square&logo=github)

---

## 📸 Funcionalidades

- ✅ **Login com Google** — cada usuário vê apenas suas próprias tarefas
- ☁️ **Sincronização em tempo real** via Firebase Firestore
- 🚀 **Regra dos 3** — 1 tarefa alta + 2 médias por dia
- ⭐ **Prioridades** — 🔴 Alta / 🟡 Média / 🟢 Baixa
- 📂 **Categorias** — Trabalho, Estudos, Casa, Contas, Saúde, Projetos, Outro
- 📅 **Prazo** e **⏱️ tempo estimado** por tarefa
- 🔄 **Status cíclico** — A fazer → Em andamento → Concluído
- 📊 **Barra de progresso** e estatísticas em tempo real
- 🔍 **Filtros** por status, prioridade e categoria

---

## 🚀 Como usar no GitHub Pages

### 1. Clone ou faça upload do arquivo
```
tada-list.html
README.md
```

### 2. Configure o Firebase (veja abaixo)

### 3. Ative o GitHub Pages
- Vá em **Settings → Pages**
- Source: `main` branch → pasta `/root`
- Acesse: `https://tadashijr.github.io/tadalist`

---

## 🔧 Configuração do Firebase

### Passo 1 — Criar o projeto
1. Acesse [console.firebase.google.com](https://console.firebase.google.com)
2. Clique em **"Adicionar projeto"**
3. Nome: `tada-list` → Criar

### Passo 2 — Ativar o Firestore
1. Menu lateral → **"Firestore Database"**
2. **"Criar banco de dados"**
3. Modo: **Teste** (30 dias)
4. Região: **southamerica-east1** (São Paulo)

### Passo 3 — Ativar Authentication com Google
1. Menu lateral → **"Authentication"**
2. **"Primeiros passos"**
3. Aba **"Método de login"** → **Google** → Ativar
4. Preencha o e-mail de suporte → **Salvar**

### Passo 4 — Registrar o app Web
1. Tela inicial do projeto → ícone **`</>`**
2. Apelido: `tada-list-web` → **Registrar**
3. Copie o objeto `firebaseConfig`

### Passo 5 — Colar as credenciais no arquivo
Abra `tada-list.html` e localize:

```js
const firebaseConfig = {
  apiKey:            "COLE_AQUI",
  authDomain:        "COLE_AQUI",
  projectId:         "COLE_AQUI",
  storageBucket:     "COLE_AQUI",
  messagingSenderId: "COLE_AQUI",
  appId:             "COLE_AQUI"
};
```

Substitua cada `"COLE_AQUI"` pelos valores copiados.

### Passo 6 — Autorizar o domínio do GitHub Pages
1. Firebase Console → **Authentication → Settings**
2. **"Domínios autorizados"** → **Adicionar domínio**
3. Cole: `SEU-USUARIO.github.io`

---

## 🔒 Regras de Segurança do Firestore

O modo de teste expira em 30 dias. Antes disso, vá em **Firestore → Regras** e substitua por:

```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /tasks/{taskId} {
      allow read, write: if request.auth != null
        && request.auth.uid == resource.data.uid;
      allow create: if request.auth != null
        && request.auth.uid == request.resource.data.uid;
    }
  }
}
```

Isso garante que cada usuário acesse **somente suas próprias tarefas**.

---

## 📁 Estrutura do projeto

```
tada-list/
├── tada-list.html   # App completo (single file)
└── README.md        # Este arquivo
```

O projeto é um **single-file app** — tudo em um único `.html`, sem dependências locais, sem build.

---

## 🛠️ Tecnologias

| Tecnologia | Uso |
|---|---|
| HTML + CSS + JS | Interface completa |
| Firebase Auth | Login com Google |
| Firebase Firestore | Banco de dados em tempo real |
| Google Fonts | Bebas Neue + DM Sans |
| GitHub Pages | Hospedagem gratuita |

---

## ❓ Problemas comuns

| Erro | Solução |
|---|---|
| `CONFIGURATION_NOT_FOUND` | Authentication não foi ativado. Veja o Passo 3. |
| Login não abre popup | Adicione o domínio nos autorizados. Veja o Passo 6. |
| Tarefas não salvam | Verifique se o Firestore está ativo e no modo teste. |
| Regras expiradas | Substitua as regras do Firestore. Veja a seção acima. |

---

## 📄 Licença

Projeto pessoal, livre para uso e modificação.
