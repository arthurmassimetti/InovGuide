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
