# 🛒 E-commerce Brasil — Processamento Assíncrono com XMLHttpRequest

> Projeto desenvolvido como parte da disciplina de Arquitetura de Interoperabilidade Web — ADS (Análise e Desenvolvimento de Sistemas)

---

## 📋 Descrição do Projeto

Este projeto implementa o processamento assíncrono de dados na página principal de um e-commerce brasileiro, utilizando o objeto nativo `XMLHttpRequest` do JavaScript para realizar requisições a APIs REST sem recarregar a página, garantindo uma experiência de usuário fluida e responsiva.

---

## 🔄 O que é o XMLHttpRequest?

O `XMLHttpRequest` (XHR) é um objeto nativo do JavaScript que permite realizar requisições HTTP de forma **assíncrona**, ou seja, sem bloquear a thread principal do navegador. Isso significa que o usuário pode continuar interagindo com a página enquanto os dados são buscados em segundo plano.

---

## ⚙️ Como funciona o ciclo de Requisição-Resposta

### 1. Ação do Usuário
Tudo começa com uma interação do usuário na página — clicar em um botão, digitar na barra de busca, etc. Esse evento dispara uma função JavaScript.

### 2. Criação do objeto XHR
```javascript
const xhr = new XMLHttpRequest();
```

### 3. Configuração da requisição
```javascript
xhr.open('GET', 'https://api.empresa.com.br/produtos', true);
// true = modo assíncrono
```

### 4. Definição dos cabeçalhos (quando necessário)
```javascript
xhr.setRequestHeader('Authorization', 'Bearer TOKEN');
xhr.setRequestHeader('Content-Type', 'application/json');
```

### 5. Registro do callback `onreadystatechange`
```javascript
xhr.onreadystatechange = function() {
  if (xhr.readyState === 4 && xhr.status === 200) {
    const dados = JSON.parse(xhr.responseText);
    atualizarInterface(dados);
  }
};
```

#### Estados do `readyState`:
| Estado | Constante         | Descrição                              |
|--------|-------------------|----------------------------------------|
| 0      | UNSENT            | Objeto criado, `open()` não chamado    |
| 1      | OPENED            | `open()` chamado                       |
| 2      | HEADERS_RECEIVED  | `send()` chamado, cabeçalhos recebidos |
| 3      | LOADING           | Corpo da resposta sendo recebido       |
| 4      | DONE              | Operação completa                      |

### 6. Envio da requisição
```javascript
xhr.send();

// Para requisições POST com body:
xhr.send(JSON.stringify({ termoBusca: 'notebook' }));
```

### 7. Atualização da interface
```javascript
function atualizarInterface(dados) {
  const lista = document.getElementById('lista-produtos');
  lista.innerHTML = dados.map(p => `<li>${p.nome} - R$${p.preco}</li>`).join('');
}
```

### 8. Tratamento de erros
```javascript
xhr.onerror = function() {
  console.error('Erro de rede na requisição.');
};
```

---

## 🚀 Como clonar o projeto localmente

### Pré-requisitos
- [Git](https://git-scm.com/downloads) instalado
- [VS Code](https://code.visualstudio.com) (recomendado)
- Conta no GitHub com acesso ao repositório

### Passo a passo

**1. Abrir o terminal**
- Windows: Git Bash ou Prompt de Comando
- macOS/Linux: Terminal nativo

**2. Navegar até a pasta desejada**
```bash
cd ~/Documentos/projetos
```

**3. Clonar o repositório**
```bash
git clone https://github.com/seu-usuario/ecommerce-xmlhttprequest.git
```

**4. Entrar na pasta do projeto**
```bash
cd ecommerce-xmlhttprequest
```

**5. Verificar o status**
```bash
git status
```

---

## 🌿 Fluxo de Trabalho Colaborativo

### Criar sua branch de trabalho
```bash
git checkout -b feature/nome-da-funcionalidade
```
> Exemplo: `git checkout -b feature/busca-assincrona`

### Enviar suas alterações
```bash
git add .
git commit -m "feat: implementa busca assíncrona com XHR"
git push origin feature/nome-da-funcionalidade
```

### Abrir um Pull Request
Acesse o repositório no GitHub → clique em **"Compare & pull request"** → solicite revisão antes de mesclar com a `main`.

---

## 📌 Boas Práticas Adotadas

- ✅ Mensagens de commit seguindo o padrão **Conventional Commits** (`feat`, `fix`, `docs`, `refactor`)
- ✅ Nunca fazer push diretamente na branch `main`
- ✅ Pull Requests obrigatórios com revisão antes do merge
- ✅ Arquivo `.gitignore` configurado (ignora `node_modules`, `.env`, configs locais)
- ✅ `README.md` sempre atualizado com instruções e documentação

---

## 🛠️ Tecnologias Utilizadas

- HTML5
- CSS3
- JavaScript (Vanilla)
- XMLHttpRequest (XHR)
- APIs REST
- Git & GitHub

---

> Disciplina: Arquitetura de Interoperabilidade Web — ADS
