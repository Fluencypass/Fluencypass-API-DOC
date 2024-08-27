# Fluencypass-API-DOC

## Como funciona a API?

A API Fluencypass utiliza arquiteturas padrão de mercado para facilitar a integração de sistemas internos, parceiros e clientes.
exemplos dessas arquiteturas que seguimos são: 
- Rest para expor os endpoints
- OAuth2 e OpenID Connect para fornecer autenticação autorização

## Autenticação 

Para utilizar a API Fluencypass você precisa de um token de acesso. Como seguimos as especificações do protocolo padrão OAuth2 e do OpenID Connect você consegue obter um token a partir de qualquer um dos fluxos disponíveis no protocolo OAuth2. Algumas possibilidades de gerar esse token incluem:
- Autenticação via SSO (Single Sign On)
- Autenticação via fluxo machine to machine (entre apis sem interação de usuários)

### Como obter um token
Em nossa api publica oferecemos por padrão 3 maneiras de obter um token (todos fluxos padronizados e disponíveis no protocolo OAuth2):
- 1. Resource Owner Password Credentials Grant
- 2. Client Credentials Grant

#### 1. Resource Owner Password Credentials Grant
Possibilita que um usuário possa fazer login a ter acesso a recursos de sua conta Fluencypass (através de endpoints disponíveis em nossa API)

**Solicitação de Token**

Envie uma solicitação POST com as credenciais do usuário para obter um token de acesso.

```
POST https://sso.fluencypass.com/realms/fluencypass/protocol/openid-connect/token
Content-Type: application/x-www-form-urlencoded

grant_type=password
&username={username}
&password={password}
&client_id={client_id}
&client_secret={client_secret}
```

*Exemplo de resposta*:
```
{
    "access_token": "<ACCESS_TOKEN>",
    "expires_in": 86400,
    "refresh_expires_in": 0,
    "token_type": "Bearer",
    "not-before-policy": 1715704038,
    "scope": "profile email"
}
```

#### 2. Client Credentials Grant
Tambem conhecido como fluxo de machine to machine esse fluxo de obtenção de token possibilita a comunicação entre a API Fluencypass e outra api sem a necessidade de login por um ser humano

**Solicitação de Token**

```
POST https://sso.fluencypass.com/realms/fluencypass/protocol/openid-connect/token
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials
&client_id={client_id}
&client_secret={client_secret}
```

*Exemplo de resposta*:
```
{
    "access_token": "<ACCESS_TOKEN>",
    "expires_in": 86400,
    "refresh_expires_in": 0,
    "token_type": "Bearer",
    "not-before-policy": 1715704038,
    "scope": "profile email"
}
```

