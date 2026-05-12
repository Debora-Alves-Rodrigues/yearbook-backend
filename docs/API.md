# API do Yearbook — Documentação de Endpoints

    Base URL (produção): `https://yearbook-backend.vercel.app`

    ## Convenções

    - Todas as respostas são em JSON
    - Rotas protegidas exigem header `Authorization: Bearer <token>`
    - O campo `senhaHash` nunca é retornado em nenhuma resposta
    - Erros seguem o formato `{ "erro": "mensagem descritiva" }`

    ## Auth

    ### POST /auth/register

    Cria uma nova conta de aluno.

    - **Autenticação:** Não
    - **Body:**

    ```json
    {
      "nome": "Maria Silva",
      "email": "maria@email.com",
      "senha": "minhasenha123",
      "cidade": "Salinas",
      "frase": "Aqui começa o futuro.",
      "planosFuturos": "Cursar Ciência da Computação na UFMG"
    }
    ```

    - **Resposta de sucesso:** `201 Created`

    ```json
    {
      "id": 1,
      "nome": "Maria Silva",
      "email": "maria@email.com",
      "cidade": "Salinas",
      "frase": "Aqui começa o futuro.",
      "planosFuturos": "Cursar Ciência da Computação na UFMG",
      "fotoUrl": null,
      "role": "USER",
      "criadoEm": "2026-04-03T10:30:00.000Z"
    }
    ```

    - **Erros:**
      - `400` — Campos obrigatórios ausentes
      - `409` — Email já cadastrado

       Autentica um aluno e retorna um token JWT.

    - **Autenticação:** Não
    - **Body:**

    ```json
    {
      "email": "maria@email.com",
      "senha": "minhasenha123"
    }
    ```

    - **Resposta de sucesso:** `200 OK`

    ```json
    {
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
    }
    ```

    - **Erros:**
      - `401` — Credenciais inválidas (email não existe ou senha incorreta)

    # Documentando /alunos

      ```json
    {
      "nome": "Maria Silva",
      "email": "maria@email.com",
      "senha": "minhasenha123",
      "cidade": "Salinas",
      "frase": "Aqui começa o futuro.",
      "planosFuturos": "Cursar Ciência da Computação na UFMG"
    }
    ```
   ## Alunos

   ### GET /alunos

    Lista todos os alunos

    - **Autenticação:** Não
    - **Body:** Nenhum

    - **Resposta de sucesso:** `200 OK`

    ```json
    {
      "id": 1,
      "nome": "Maria Tereza",
      "email": "maria@email.com",
      "cidade": "Cristália",
      "frase": "Nunca desistir",
      "planosFuturos": "Cursar Engenharia Aeroespacial na UFMG",
      "fotoUrl": null,
      "role": "USER",
      "criadoEm": "2026-04-03T10:30:00.000Z"
    },
    {
      "id": 2,
      "nome": "Isabelle Cardoso",
      "email": "bell@email.com",
      "cidade": "Taiobeiras",
      "frase": "Ler é crescer",
      "planosFuturos": "Cursar Letras na UFMG",
      "fotoUrl": null,
      "role": "USER",
      "criadoEm": "2026-04-04T10:40:00.000Z"
    }
    ```

   ### GET /alunos/:id

    Busca um aluno pelo ID

    - **Autenticação:** Não
    - **Body:** Nenhum

    - **Resposta de sucesso:** `200 OK`

    ```json
    {
      "id": 1,
      "nome": "Maria Tereza",
      "email": "maria@email.com",
      "cidade": "Cristália",
      "frase": "Nunca desistir",
      "planosFuturos": "Cursar Engenharia Aeroespacial na UFMG",
      "fotoUrl": null,
      "role": "USER",
      "criadoEm": "2026-04-03T10:30:00.000Z"
    }
    ```

    - **Erros:**
      - `404` — ID não encontrado (ID inexistente)

   ### PUT /alunos/:id

    Atualiza o próprio perfil

    - **Autenticação:** Bearer token
    - **Body:** 

    ```json
    {
      "nome": "Débora Alves",
      "cidade": "Salinas",
      "frase":"Tudo posso Naquele que me fortalece",
      "planosFuturos": "Ir para a faculdade",
      "fotoURL": null,
    }
    ```
   - **Resposta de sucesso:** `200 OK`

   - **Erros:**
      - `401` — Não logado
      - `403` — Tentando atualizar o perfil de outra pessoa
   
   ### DELETE /alunos/:id

    Remove um aluno

    - **Autenticação:** Bearer token (admin)
    - **Body:** Não

    - **Resposta de sucesso:** `204´

    - **Erros:**
      - `401` — Não logado
      - `403` — Não é admin.

  


  



