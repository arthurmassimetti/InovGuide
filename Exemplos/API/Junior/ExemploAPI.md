## - **Passo 1: Criar o ambiente do projeto**
# Crie uma pasta para o projeto e navegue até ela:

```bash
mkdir api-example-native - criar a pasta no diretorio que estiver
cd api-example-native - mudar do diretorio que está para a pasta que foi criada
```

## **Inicialize o projeto:**

```bash
npm init -y - instala todas as dependencias do node de forma eficiente com o -y
```

---

## **Código de Exemplo**

```javascript
// Importando o módulo https
const https = require('https');

// URL da API
const API_URL = 'https://jsonplaceholder.typicode.com/posts';

// Função para fazer a requisição à API
function fetchPosts() {
  https.get(API_URL, (res) => {
    let data = '';

    // Concatena os pedaços de dados recebidos
    res.on('data', (chunk) => {
      data += chunk;
    });

    // Quando todos os dados forem recebidos
    res.on('end', () => {
      try {
        // Converter os dados recebidos em JSON
        const posts = JSON.parse(data);

        // Exibir os primeiros 5 posts
        console.log('Lista de Posts:');
        posts.slice(0, 5).forEach(post => {
          console.log(`ID: ${post.id}, Título: ${post.title}`);
        });
      } catch (error) {
        console.error('Erro ao processar os dados:', error.message);
      }
    });
  }).on('error', (err) => {
    console.error('Erro na requisição:', err.message);
  });
}

// Executando a função
fetchPosts();
```

## Resumo do Código

O código realiza as seguintes etapas:

1. **Define a URL da API**: Utiliza o endpoint `https://jsonplaceholder.typicode.com/posts` para buscar uma lista de posts fictícios.
2. **Faz uma requisição HTTP**:
   - Usa `https.get()` para enviar a requisição ao servidor.
   - Recebe os dados em partes (*chunk*) e os concatena em uma string.
3. **Processa a resposta**:
   - Converte a string JSON recebida para um objeto JavaScript com `JSON.parse()`.
   - Exibe os 5 primeiros posts, mostrando o ID e o título.
4. **Trata erros**:
   - Captura erros de conexão ou requisição com `on('error')`.
   - Utiliza `try-catch` para tratar erros ao manipular os dados.

## Resultado Esperado

Ao executar o código, o terminal exibirá uma lista dos primeiros 5 posts retornados pela API. Cada post apresenta o **ID** e o **título**, organizados de forma simples.

### **Exemplo de Saída**

```plaintext
Lista de Posts:
ID: 1, Título: sunt aut facere repellat provident occaecati excepturi optio reprehenderit
ID: 2, Título: qui est esse
ID: 3, Título: ea molestias quasi exercitationem repellat qui ipsa sit aut
ID: 4, Título: eum et est occaecati
ID: 5, Título: nesciunt quas odio
```

---
