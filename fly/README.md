# stacks-graphql-api

The demo version of stacks-graphql-api is deployed on fly.io.

## Deployment

1. Set the secrets

```sh
cd fly
flyctl secrets set \
HASURA_GRAPHQL_DATABASE_URL="postgres://user:pass@serverhost.com:5432/databasename" \
HASURA_GRAPHQL_ADMIN_SECRET="OurAdminSecret"
```

2. Disable autoscaling

```sh
flyctl autoscale disable
```

3. Deploy

```sh
flyctl deploy
```

4. Apply the metadata to the deployed hasura instance

```sh
cd stacks-graphql-api
hasura metadata apply --endpoint https://my-endpoint --admin-secret "OurAdminSecret"
```
