# BlueSkyAPI

# Documentação da API para Consulta de Perfis e Publicações do BlueSky

## Introdução

Esta documentação descreve as APIs fornecidas para interagir com perfis e publicações na plataforma Bluesky. Estas APIs permitem a resolução de IDs descentralizados (DID), recuperação de informações de perfil, obtenção de posts, além de pesquisa de perfis e publicações.

### Limitações Gerais

- O valor máximo do limite (`limit`) para todos os endpoints descritos é **100**, com exceção da API de detalhes de um post específico, onde o limite é **1000**.
- Os exemplos de limites fornecidos nesta documentação são aqueles que são comumente carregados pelo site e são menores que os valores máximos.

## Resolução de DID

### Descrição

A primeira etapa para interagir com um perfil é resolver o Identificador Descentralizado (DID) a partir de um handle específico (nome de usuário).

### Endpoint

`GET https://public.api.bsky.app/xrpc/com.atproto.identity.resolveHandle?handle={handle}`

### Parâmetros

- `handle`: Substitua `{handle}` pelo handle do perfil desejado. Exemplo: `bsky.app`.

### Exemplo de Resposta

```json
{
  "did": "did:plc:z72i7hdynmk6r22z27h6tvur"
}
```

Este DID é fundamental para acessar outras informações relacionadas ao perfil.

## Consulta de Informações do Perfil

### Descrição

Recupere informações detalhadas do perfil usando o DID obtido anteriormente.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.actor.getProfile?actor={did}&filter=posts_and_author_threads&limit=1`

### Parâmetros

- `actor`: Substitua `{did}` pelo DID do perfil. Todos os `:` no DID devem ser substituídos por `%3A`.

### Exemplo de URL

Se o DID for `did:plc:gorq7i3msirfgxrxc6kklnl7`, a URL será:

```
https://public.api.bsky.app/xrpc/app.bsky.actor.getProfile?actor=did%3Aplc%3Agorq7i3msirfgxrxc6kklnl7&filter=posts_and_author_threads&limit=1
```

## Obtenção de Posts do Perfil

### Descrição

Recupere as publicações feitas por um perfil específico.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.feed.getAuthorFeed?actor={did}&filter=posts_and_author_threads&limit={limit}`

### Parâmetros

- `actor`: Substitua `{did}` pelo DID do perfil.
- `limit`: Define o número máximo de posts a serem retornados. O valor máximo é `100`.

### Exemplo de URL

```
https://public.api.bsky.app/xrpc/app.bsky.feed.getAuthorFeed?actor=did%3Aplc%3Agorq7i3msirfgxrxc6kklnl7&filter=posts_and_author_threads&limit=30
```

## Obtenção de Posts com Mídia

### Descrição

Recupere as publicações contendo mídia feitas por um perfil específico.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.feed.getAuthorFeed?actor={did}&filter=posts_with_media&limit={limit}`

### Parâmetros

- `actor`: Substitua `{did}` pelo DID do perfil.
- `limit`: Define o número máximo de posts a serem retornados. O valor máximo é `100`.

### Exemplo de URL

```
https://public.api.bsky.app/xrpc/app.bsky.feed.getAuthorFeed?actor=did%3Aplc%3Aqrlodsav63erq6ukjv7slvp3&filter=posts_with_media&limit=30
```

## Obtenção de Seguidores

### Descrição

Recupere a lista de seguidores de um perfil específico.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.graph.getFollowers?actor={did}&limit={limit}`

### Parâmetros

- `actor`: Substitua `{did}` pelo DID do perfil.
- `limit`: Define o número máximo de seguidores a serem retornados. O valor máximo é `100`.

### Exemplo de URL

```
https://public.api.bsky.app/xrpc/app.bsky.graph.getFollowers?actor=did%3Aplc%3Aqrlodsav63erq6ukjv7slvp3&limit=30
```

## Pesquisa de Perfis

### Descrição

Permite pesquisar perfis utilizando um termo específico.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.actor.searchActorsTypeahead?q={termo}&limit={limit}`

### Parâmetros

- `q`: Substitua `{termo}` pelo termo de pesquisa.
- `limit`: Define o número máximo de resultados a serem retornados. O valor máximo é `100`.

### Exemplo de URL

```
https://public.api.bsky.app/xrpc/app.bsky.actor.searchActorsTypeahead?q=anime&limit=8
```

## Pesquisa de Posts Populares

### Descrição

Permite pesquisar por posts populares utilizando um termo específico.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.feed.searchPosts?q={termo}&limit={limit}&sort=top`

### Parâmetros

- `q`: Substitua `{termo}` pelo termo de pesquisa.
- `limit`: Define o número máximo de resultados a serem retornados. O valor máximo é `100`.

### Exemplo de URL

```
https://public.api.bsky.app/xrpc/app.bsky.feed.searchPosts?q=anime&limit=25&sort=top
```

## Pesquisa de Últimos Posts

### Descrição

Permite pesquisar pelos últimos posts utilizando um termo específico.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.feed.searchPosts?q={termo}&limit={limit}&sort=latest`

### Parâmetros

- `q`: Substitua `{termo}` pelo termo de pesquisa.
- `limit`: Define o número máximo de resultados a serem retornados. O valor máximo é `100`.

### Exemplo de URL

```
https://public.api.bsky.app/xrpc/app.bsky.feed.searchPosts?q=anime&limit=25&sort=latest
```

## Geradores de Feed Populares

### Descrição

Recupere uma lista de geradores de feed populares baseados em um termo específico.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.unspecced.getPopularFeedGenerators?limit={limit}&query={termo}`

### Parâmetros

- `query`: Substitua `{termo}` pelo termo de pesquisa.
- `limit`: Define o número máximo de resultados a serem retornados. O valor máximo é `100`.

### Exemplo de URL

```
https://public.api.bsky.app/xrpc/app.bsky.unspecced.getPopularFeedGenerators?limit=15&query=anime
```

## Obtenção de Detalhes de um Post Específico

### Descrição

Recupere os detalhes de uma postagem específica utilizando o URI do post.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.feed.getPostThread?uri={uri}&depth={depth}`

### Parâmetros

- `uri`: Substitua `{uri}` pelo URI do post.
- `depth`: Define a profundidade da thread a ser retornada. O valor máximo é `1000`.

### Exemplo de Construção de URL

Dado o link do post `https://bsky.app/profile/brunosa.bsky.social/post/3l33tt4rv762p`, a URL se tornará:

```
https://public.api.bsky.app/xrpc/app.bsky.feed.getPostThread?uri=at%3A%2F%2Fbrunosa.bsky.social%2Fapp.bsky.feed.post%2F3l33tt4rv762p&depth=10
```

Outros exemplos:

1. Post: `https://bsky.app/profile/adribangtancafe.bsky.social/post/3l33nfz4qxy2v`
   URL:
   ```
   https://public.api.bsky.app/xrpc/app.bsky.feed.getPostThread?uri=at%3A%2F%2Fadribangtancafe.bsky.social%2Fapp.bsky.feed.post%2F3l33nfz4qxy2v&depth=10
   ```

2. Post: `https://bsky.app/profile/farofa.com.br/post/3l33ldwwlcc25`
   URL:
   ```
   https://public.api.bsky.app/xrpc/app.bsky.feed.getPostThread?uri=at%3A%2F%2Ffarofa.com.br%2Fapp.bsky.feed.post%2F3l33ldwwlcc25&depth=10
