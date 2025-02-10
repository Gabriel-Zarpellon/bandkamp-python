# BandKamp
## Descrição do projeto

Este projeto é constituído de uma API desenvolvida com base em testes, como atividade do módulo de Python da Kenzie Academy.

A API consiste na criação, login e gerenciamento de usuários e na criação e gerenciamento de álbuns e músicas, utilizando Generic Views para seu funcionamento.

## Rotas de usuários

### Registro de usuário POST /users/
Padrão de corpo

```json
{
  "username": "xNAFnDenYsuhJaD",
  "email": "user@example.com",
  "password": "string",
  "full_name": "string",
  "artistic_name": "string"
}
```

Padrão de resposta (STATUS 201)

```json
{
  "id": 0,
  "username": "4JBZEc2V7m.pdyTrO.kgtQqVtaOo",
  "email": "user@example.com",
  "full_name": "string",
  "artistic_name": "string"
}
```

#### Possíveis erros

400 BAD REQUEST - Campos ausentes

```json
{
  "username": [
     "This field is required."
   ],
  "email": [
     "This field is required."
   ],
  "password": [
     "This field is required."
   ],
  "artistic_name": [
     "This field is required."
   ]
}
```

STATUS 400 - Email ou username já cadastrados

```json
{
  "username": [
     "A user with that username already exists."
   ],
  "email": [
     "user with this email already exists."
   ]
}
```

### Login de usuário POST /users/login/
Padrão de corpo

```json
{
  "username": "string",
  "password": "string"
}
```

Padrão de resposta (STATUS 200)

```json
{
  "access": "string",
  "refresh": "string"
}
```

### Possíveis erros

401 Unauthorized - Credenciais inválidas

```json
{
  "detail": "No active account found with the given credentials"
}
```

400 BAD REQUEST - Campos ausentes

```json
{
  "username": [
     "This field is required."
   ],
  "email": [
     "This field is required."
   ]
}
```

### Acessar perfil de usuário GET /users/<int:user_id>/

Padrão de resposta (STATUS: 200)

```json
{
  "id": 0,
  "username": "HunFlOOq0IDgJVTRjDhYeiyRV.wf9wZbZpBO_mca@kTosBcy1GknZuZGqMg.ROj7T@NA5gvXp",
  "email": "user@example.com",
  "full_name": "string",
  "artistic_name": "string"
}
```

### Possíveis erros

404 Not found - Usuário não encontrado

```json
{
  "detail": "No User matches the given query."
}
```

### Atualizar perfil de usuário PATCH /users/<int:user_id>/ - esta rota requer autorização de administrador ou dono do perfil
Padrão de corpo - os campos dessa requisição são todos opcionais

```json
{
  "username": "8R+MI.u6TYdB5kbrVD3sDM-pfTdN0dy-7t7HRFpiTJv1rvlk",
  "email": "user@example.com",
  "password": "string",
  "full_name": "string",
  "artistic_name": "string"
}
```

Padrão de resposta (STATUS 200)

```json
{
  "id": 0,
  "username": "idyAPHeo@cHdVZ2Sb7LPRix+gWx3gPO.@6fvS9APuizJ48zJ.lUvmTRan3zVXiNQg",
  "email": "user@example.com",
  "full_name": "string",
  "artistic_name": "string"
}
```

### Possíveis erros

401 Unauthorized - Credenciais ausentes

```json
{
  "detail": "Authentication credentials were not provided."
}
```

403 Forbidden - Usuário sem permissão

```json
{
  "detail": "You do not have permission to perform this action."
}
```

404 Not found - Usuário não encontrado

```json
{
  "detail": "No User matches the given query."
}
```

### Excluir perfil de usuário DELETE /users/<int:user_id>/ - esta rota requer autorização de administrador ou dono do perfil
Padrão de corpo - os campos dessa requisição são todos opcionais

Esta rota não tem um corpo de resposta (STATUS: 204)

### Possíveis erros

401 Unauthorized - Credenciais ausentes

```json
{
  "detail": "Authentication credentials were not provided."
}
```

403 Forbidden - Usuário sem permissão

```json
{
  "detail": "You do not have permission to perform this action."
}
```

404 Not found - Usuário não encontrado

```json
{
  "detail": "No User matches the given query."
}
```

## Rotas de álbuns

### Registro de álbum POST /albums/ - Esta rota requer autenticação
Padrão de corpo

```json
{
  "name": "string",
  "year": 32767
}
```

Padrão de resposta (STATUS 201)

```json
{
  "id": 0,
  "name": "string",
  "year": 32767,
  "user": {
    "id": 0,
    "username": "ZapAGUsl4k_G1EgwwSgeR9wtZ@PmLgWiljRaCHicEnDAgKrMf389-nznKrAR26WWrrhlpqeqcjBnPqWHxt2Vp2dae8NS",
    "email": "user@example.com",
    "full_name": "string",
    "artistic_name": "string"
  }
}
```

### Possíveis erros

401 Unauthorized - Credenciais ausentes

```json
{
  "detail": "Authentication credentials were not provided."
}
```

400 BAD REQUEST - Campos ausentes

```json
{
  "name": [
    "This field is required."
   ],
  "year": [
    "This field is required."
   ]
}
```

### Leitura de álbuns GET /albums/

Padrão de resposta (STATUS: 200)

```json
{
  "count": 123,
  "next": "http://api.example.org/accounts/?page=4",
  "previous": "http://api.example.org/accounts/?page=2",
  "results": [
    {
      "id": 0,
      "name": "string",
      "year": 32767,
      "user": {
        "id": 0,
        "username": "FfgC@zf8o8MloTo-+R.peOOeE8SXegRsKm8jWQxu_",
        "email": "user@example.com",
        "full_name": "string",
        "artistic_name": "string"
      }
    }
  ]
}
```

## Criação de música POST /albums/<int:album_id>/songs/ - Esta rota requer autenticação
Padrão de corpo

```json
{
  "title": "string",
  "duration": "string"
}
```

Padrão de resposta (STATUS: 201)

```json
{
  "id": 0,
  "title": "string",
  "duration": "string",
  "album_id": 0
}
```

### Possíveis erros

401 Unauthorized - Credenciais ausentes

```json
{
  "detail": "Authentication credentials were not provided."
}
```

404 Not found - Álbum não encontrado

```json
{
  "detail": "No Album matches the given query."
}
```

400 BAD REQUEST - Campos ausentes

```json
{
  "title": [
    "This field is required."
   ],
  "duration": [
    "This field is required."
   ]
}
```


### Leitura de músicas por álbum GET /albums/<int:album_id>/songs

Padrão de resposta (STATUS: 200)

```json
{
  "count": 123,
  "next": "http://api.example.org/accounts/?page=4",
  "previous": "http://api.example.org/accounts/?page=2",
  "results": [
    {
      "id": 0,
      "title": "string",
      "duration": "string",
      "album_id": 0
    }
  ]
}
```
### Possíveis erros

404 Not found - Álbum não encontrado

```json
{
  "detail": "No Album matches the given query."
}
```

## Rota de documentação

localhost:8000/api/docs/swagger-ui/


## Preparando ambiente para execução dos testes

1. Verifique se os pacotes **pytest**, **pytest-testdox** e/ou **pytest-django** estão instalados globalmente em seu sistema:
```shell
pip list
```

2. Caso eles apareçam na listagem, rode os comandos abaixo para realizar a desinstalação:

```shell
pip uninstall pytest pytest-testdox pytest-django -y
```

3. Após isso, crie seu ambiente virtual:
```shell
python -m venv venv
```

4. Ative seu ambiente virtual:

```shell
# Linux e Mac:
source venv/bin/activate

# Windows (PowerShell):
.\venv\Scripts\activate

# Windows (GitBash):
source venv/Scripts/activate
```

5. Instale as bibliotecas necessárias:

```shell
pip install pytest-testdox pytest-django
```


## Execução dos testes:

Como este projeto se trata de uma refatoração, não terá divisão de testes por tarefa, pois o objetivo é que todos os testes continuem passando após a refatoração.
Deste modo, para rodar a bateria de todos os testes, utilize:
```shell
pytest --testdox -vvs
```
---

Caso você tenha interesse em rodar apenas um diretório de testes específico, utilize os comandos abaixo:

Users:
```python
pytest --testdox -vvs tests/users/
```

Albums:
```python
pytest --testdox -vvs tests/albums/
```

Songs:
```python
pytest --testdox -vvs tests/songs/
```

---

Você também pode rodar cada método de teste isoladamente:

```shell
pytest --testdox -vvs caminho/para/o/arquivo/de/teste::NomeDaClasse::nome_do_metodo_de_teste
```

**Exemplo**: executar somente "test_user_login_without_required_fields".

```shell
pytest --testdox -vvs tests/users/test_login_view.py::UserLoginViewTest::test_user_login_without_required_fields
```
