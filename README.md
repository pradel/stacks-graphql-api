<div align="center">

<h1>stacks-graphql-api</h1>
<p>A GraphQL API to query the Stacks blockchain.</p>

</div>

## Features

- Query the Stacks blockchain using a GraphQL API.
- Create complex queries including relations, pagination, sorting, and filtering.
- Realtime updates via GraphQL subscriptions.
- Blazing fast, using [Hasura](https://github.com/hasura/graphql-engine).

## Installation

TODO.

## Usage example

### Queries

Get the last 10 blocks mined with the number of transactions included in that block:

```graphql
{
  blocks_connection(first: 10, order_by: { block_height: desc }) {
    edges {
      node {
        block_height
        block_hash
        burn_block_time
        burn_block_hash
        burn_block_height
        # Number of transactions included in the block
        transactions_aggregate {
          aggregate {
            count
          }
        }
      }
    }
  }
}
```

### Subscriptions

Receive an event when a new block is mined:

```graphql
subscription {
  blocks_connection(first: 1, order_by: {block_height: desc}) {
    edges {
      node {
        block_height
        burn_block_time
        transactions_aggregate {
          aggregate {
            count
          }
        }
      }
    }
  }
```

## Contributing

Do you have an idea or want to contribute? Pull requests are very welcome!

## Known limitations

- No support for balances
- Some tables are not tracked and exposed yet
- No clean views to convert "bytea" to "hex" in the query response as well as the "where" arguments - Hasura does not support Materialized Views for relay https://github.com/hasura/graphql-engine/issues/7013

## License

MIT License © [Léo Pradel](https://www.leopradel.com/)
