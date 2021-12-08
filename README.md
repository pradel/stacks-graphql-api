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

Get the data of transaction `0x5cca607a5fa44855e2b56dd4fc41a53b871c1f75eecbf5e271c2d6439e32b745`:

```graphql
{
  transactions_connection(
    where: {
      tx_id: {
        _eq: "\\x5cca607a5fa44855e2b56dd4fc41a53b871c1f75eecbf5e271c2d6439e32b745"
      }
    }
  ) {
    edges {
      node {
        id
        sender_address
        fee_rate
        nonce
        contract_call_contract_id
        contract_call_function_name
        contract_call_function_args
        contract_call {
          source_code
          tx_id
        }
        block {
          block_hash
          block_height
          burn_block_time
          burn_block_hash
          burn_block_height
        }
        ft_events {
          asset_event_type_id
          asset_identifier
          sender
          recipient
        }
        nft_events {
          asset_event_type_id
          asset_identifier
          sender
          recipient
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
```

## Contributing

Do you have an idea or want to contribute? Pull requests are very welcome!

## Known limitations

- No support for balances
- Some tables are not tracked and exposed yet
- No clean views to convert "bytea" to "hex" in the query response as well as the "where" arguments - Hasura does not support Materialized Views for relay yet https://github.com/hasura/graphql-engine/issues/5044

## License

MIT License © [Léo Pradel](https://www.leopradel.com/)
