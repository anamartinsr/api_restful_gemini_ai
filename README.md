# Api Rest com Google Gemini 

O objetivo do projeto é criar uma API RESTful para gerenciar posts, com funcionalidades para listar, criar, atualizar posts e realizar upload de imagens. Além disso, a descrição das imagens é gerada automaticamente com a integração da API **Google Gemini**.

## Funcionalidades

- **Listar Posts**: Exibe todos os posts armazenados no banco de dados.
- **Criar Post**: Permite a criação de novos posts através de uma API REST.
- **Upload de Imagem**: Permite o upload de imagens associadas a um novo post.
- **Atualizar Post**: Permite a atualização de um post, incluindo o processamento de uma imagem para gerar uma descrição automática usando a API **Gemini da Google**.

## Tecnologias Utilizadas

- **Node.js**: Ambiente de execução JavaScript para servidores.
- **Express.js**: Framework para criação de APIs RESTful.
- **MongoDB**: Banco de dados NoSQL para armazenamento dos posts.
- **Google Gemini (Generative AI)**: API para gerar descrições automáticas de imagens.
- **Multer**: Middleware para processamento de upload de arquivos (imagens).
- **FS (File System)**: Módulo Node.js para manipulação de arquivos, usado para mover imagens carregadas.

## Como Rodar o Projeto

### Pré-requisitos

- **Node.js** instalado na sua máquina.
- **MongoDB Atlas** configurado para persistência dos dados.
- **Chave de API do Google Gemini** para gerar descrições de imagens.

### Passo a Passo:

1. **Clone o repositório:**

   ```bash
   git clone https://github.com/anamartinsr/api_restful_gemini_ai.git
   ```
2. **Instale as dependências:**
   ```bash
   npm install
   ```
3. **Crie um arquivo .env na raiz do projeto com a seguinte chave (substitua pelo seu valor real):**
   ```bash
   GEMINI_API_KEY=<sua_chave_api_google>
   MONGO_URI=<string_de_conexao_com_o_banco_de_dados>
   ```
4. **Inicie o servidor:**
   ```bash
   npm start
   ```

## Endpoints da API
### 1. **Listar Posts**
- **Método**: `GET`
- **Rota**: `/posts`
- **Descrição**: Retorna todos os posts existentes no banco de dados.
- **Exemplo de Resposta**:
  ```json
  [
    {
      "id": "1",
      "descricao": "Texto do post",
      "imgUrl": "http://localhost:3000/imagem.jpg",
      "alt": "Texto alternativo da imagem"
    },
    ...
  ]
### 2. **Criar Novo Post**
- **Método**: `POST`
- **Rota**: `/posts`
- **Exemplo de Resposta**:
  ```json
  {
    "descricao": "Texto do post",
    "imgUrl": "URL da imagem",
    "alt": "Texto alternativo"
  }

- **Descrição**: Cria um novo post com a descrição fornecida. Retorna os dados do post recém-criado.
- **Exemplo de Resposta**:
  ```json
    {
      "id": "2",
      "descricao": "Texto do novo post",
      "imgUrl": "http://localhost:3000/imagem.jpg",
      "alt": "Texto alternativo"
    }
  ```
### 3. **Upload de Imagem**
- **Método**: `POST`
- **Rota**: `/upload`
- **Body (FormData)**: Envie a imagem com o campo nomeado como "imagem".
- **Exemplo**: envie um arquivo de imagem no campo imagem.

- **Descrição**: Faz o upload de uma imagem e cria um post associado a ela. A imagem será salva na pasta uploads/ no servidor, com o nome original do arquivo.

- **Exemplo de Resposta**:
  ```json
    {
      "id": "3",
      "descricao": "Texto do post",
      "imgUrl": "http://localhost:3000/uploads/imagem.jpg",
      "alt": "Texto alternativo"
    }
  ```
### 4. **Atualizar Post**
- **Método**: `PUT`
- **Rota**: `/upload/:id`
**Body (JSON):**
  ```json
    {
      "alt": "Novo texto alternativo"
    }
  ```

- **Descrição**: Atualiza o post identificado pelo id. Esse endpoint permite que a descrição da imagem seja gerada automaticamente usando a API Gemini e associada ao post.
- **Exemplo de Resposta**:
  ```json
    {
      "id": "3",
      "descricao": "Nova descrição gerada automaticamente",
      "imgUrl": "http://localhost:3000/uploads/imagem.jpg",
      "alt": "Novo texto alternativo"
    }
  ```
