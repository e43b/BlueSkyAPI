# BlueSkyAPI: API Documentation for Profile and Post Queries on BlueSky

English | [Português](README_pt.md)

## Introduction

This documentation outlines the APIs provided for interacting with profiles and posts on the Bluesky platform. These APIs allow for the resolution of Decentralized Identifiers (DID), retrieval of profile information, fetching of posts, as well as searching for profiles and posts.

### General Limitations

- The maximum value for the `limit` parameter across all endpoints described here is **100**, except for the API that fetches details of a specific post, where the limit is **1000**.
- The limit examples provided in this documentation are those commonly used by the site, which are lower than the maximum allowed values.

## DID Resolution

### Description

The first step to interact with a profile is to resolve the Decentralized Identifier (DID) from a specific handle (username).

### Endpoint

`GET https://public.api.bsky.app/xrpc/com.atproto.identity.resolveHandle?handle={handle}`

### Parameters

- `handle`: Replace `{handle}` with the desired profile handle. Example: `bsky.app`.

### Example Response

```json
{
  "did": "did:plc:z72i7hdynmk6r22z27h6tvur"
}
```

This DID is essential for accessing other profile-related information.

## Profile Information Query

### Description

Retrieve detailed profile information using the previously obtained DID.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.actor.getProfile?actor={did}&filter=posts_and_author_threads&limit=1`

### Parameters

- `actor`: Replace `{did}` with the profile's DID. All `:` in the DID must be replaced with `%3A`.

### Example URL

If the DID is `did:plc:gorq7i3msirfgxrxc6kklnl7`, the URL would be:

```
https://public.api.bsky.app/xrpc/app.bsky.actor.getProfile?actor=did%3Aplc%3Agorq7i3msirfgxrxc6kklnl7&filter=posts_and_author_threads&limit=1
```

## Fetching Profile Posts

### Description

Retrieve posts made by a specific profile.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.feed.getAuthorFeed?actor={did}&filter=posts_and_author_threads&limit={limit}`

### Parameters

- `actor`: Replace `{did}` with the profile's DID.
- `limit`: Sets the maximum number of posts to be returned. The maximum value is `100`.

### Example URL

```
https://public.api.bsky.app/xrpc/app.bsky.feed.getAuthorFeed?actor=did%3Aplc%3Agorq7i3msirfgxrxc6kklnl7&filter=posts_and_author_threads&limit=30
```

## Fetching Posts with Media

### Description

Retrieve posts containing media made by a specific profile.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.feed.getAuthorFeed?actor={did}&filter=posts_with_media&limit={limit}`

### Parameters

- `actor`: Replace `{did}` with the profile's DID.
- `limit`: Sets the maximum number of posts to be returned. The maximum value is `100`.

### Example URL

```
https://public.api.bsky.app/xrpc/app.bsky.feed.getAuthorFeed?actor=did%3Aplc%3Aqrlodsav63erq6ukjv7slvp3&filter=posts_with_media&limit=30
```

## Fetching Followed Profiles

### Description

Retrieve the list of profiles followed by a specific profile.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.graph.getFollows?actor={did}&limit={limit}`

### Parameters

- `actor`: Replace `{did}` with the profile's DID.
- `limit`: Sets the maximum number of followed profiles to be returned. The maximum value is `100`.

### Example URL

```
https://public.api.bsky.app/xrpc/app.bsky.graph.getFollows?actor=did%3Aplc%3Aqrlodsav63erq6ukjv7slvp3&limit=30
```

## Fetching Followers

### Description

Retrieve the list of followers for a specific profile.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.graph.getFollowers?actor={did}&limit={limit}`

### Parameters

- `actor`: Replace `{did}` with the profile's DID.
- `limit`: Sets the maximum number of followers to be returned. The maximum value is `100`.

### Example URL

```
https://public.api.bsky.app/xrpc/app.bsky.graph.getFollowers?actor=did%3Aplc%3Aqrlodsav63erq6ukjv7slvp3&limit=30
```

## Profile Search

### Description

Search for profiles using a specific term.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.actor.searchActorsTypeahead?q={term}&limit={limit}`

### Parameters

- `q`: Replace `{term}` with the search term.
- `limit`: Sets the maximum number of results to be returned. The maximum value is `100`.

### Example URL

```
https://public.api.bsky.app/xrpc/app.bsky.actor.searchActorsTypeahead?q=anime&limit=8
```

## Search for Popular Posts

### Description

Search for popular posts using a specific term.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.feed.searchPosts?q={term}&limit={limit}&sort=top`

### Parameters

- `q`: Replace `{term}` with the search term.
- `limit`: Sets the maximum number of results to be returned. The maximum value is `100`.

### Example URL

```
https://public.api.bsky.app/xrpc/app.bsky.feed.searchPosts?q=anime&limit=25&sort=top
```

## Search for Latest Posts

### Description

Search for the latest posts using a specific term.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.feed.searchPosts?q={term}&limit={limit}&sort=latest`

### Parameters

- `q`: Replace `{term}` with the search term.
- `limit`: Sets the maximum number of results to be returned. The maximum value is `100`.

### Example URL

```
https://public.api.bsky.app/xrpc/app.bsky.feed.searchPosts?q=anime&limit=25&sort=latest
```

## Popular Feed Generators

### Description

Retrieve a list of popular feed generators based on a specific term.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.unspecced.getPopularFeedGenerators?limit={limit}&query={term}`

### Parameters

- `query`: Replace `{term}` with the search term.
- `limit`: Sets the maximum number of results to be returned. The maximum value is `100`.

### Example URL

```
https://public.api.bsky.app/xrpc/app.bsky.unspecced.getPopularFeedGenerators?limit=15&query=anime
```

## Fetching Specific Post Details

### Description

Retrieve the details of a specific post using the post's URI.

### Endpoint

`GET https://public.api.bsky.app/xrpc/app.bsky.feed.getPostThread?uri={uri}&depth={depth}`

### Parameters

- `uri`: Replace `{uri}` with the post's URI.
- `depth`: Sets the depth of the thread to be returned. The maximum value is `1000`.

### Example URL Construction

Given the post link `https://bsky.app/profile/brunosa.bsky.social/post/3l33tt4rv762p`, the URL would become:

```
https://public.api.bsky.app/xrpc/app.bsky.feed.getPostThread?uri=at%3A%2F%2Fbrunosa.bsky.social%2Fapp.bsky.feed.post%2F3l33tt4rv762p&depth=10
```

Other examples:

1. Post: `https://bsky.app/profile/adribangtancafe.bsky.social/post/3l33nfz4qxy2v`
   URL:
   ```
   https://public.api.bsky.app/xrpc/app.bsky.feed.getPostThread?uri=at%3A%2F%2Fadribangtancafe.bsky.social%2Fapp.bsky.feed.post%2F3l33nfz4qxy2v&depth=10
   ```

2. Post: `https://bsky.app/profile/farofa.com.br/post/3l33ldwwlcc25`
   URL:
   ```
   https://public.api.bsky.app/xrpc/app.bsky.feed.getPostThread?uri=at%3A%2F%2Ffarofa.com.br%2Fapp.bsky.feed.post%2F3l33ldwwlcc25&depth=10
