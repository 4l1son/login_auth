# Sistema de Login usando Autenticação via Token

## Tecnologias Utilizadas
[![Laravel Logo](https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg)](https://laravel.com)

## Sobre o Projeto

Desenvolver um sistema de autenticação usando tokens para proteger endpoints de uma API em PHP.

### Estrutura do Projeto

#### Controller `AuthController`:

- Método `login`:
  - Recebe as credenciais (email e senha) do usuário.
  - Valida as credenciais usando o Eloquent (método `attempt`).
  - Gera um token JWT válido se as credenciais são autenticadas com sucesso.
  - Retorna o token como resposta em formato JSON.

#### Middleware `auth:api`:

- Protege endpoints da API exigindo um token válido.
- Usado em rotas onde a autenticação é necessária.

#### Model `User`:

- Representa os usuários no banco de dados.
- Pode incluir relacionamentos com outras entidades, dependendo das necessidades.

#### Factory `UserFactory`:

- Gera dados de usuário de teste para uso em seeds.

#### Seeder `DatabaseSeeder`:

- Usa a factory para criar instâncias de usuário no banco de dados.

#### Rota Protegida:

- Pode ser qualquer rota que exija autenticação.
- Use o middleware `auth:api` para proteger o acesso a essas rotas.

#### Resposta JSON com Token:

- O token JWT é incluído na resposta após uma autenticação bem-sucedida.
- O token é utilizado nas requisições subsequentes para autenticar o usuário.

### Fluxo de Autenticação:

- O cliente faz uma solicitação de login (POST para `/api/login`) com credenciais.
- Exemplo de solicitação:
```bash
curl -X POST   http://127.0.0.1:8000/api/login   -H 'Accept: application/json'   -d 'email=mills.birdie@example.net&password=password'

Resposta com JSON token

{
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
  "token_type": "bearer",
  "expires_in": 3600
}
