# as-boilerplate Smart Contract

A [smart contract] written in [AssemblyScript] for an app initialized with [create-near-app]

# Quick Start

Before you compile this code, you will need to install [Node.js] ≥ 12

# Exploring The Code

1. The main smart contract code lives in `assembly/index.ts`. You can compile this code by navigating into the contract folder by typing and running `asb` or `yarn build` in the contract folder.

[smart contract]: https://docs.near.org/docs/develop/contracts/overview
[assemblyscript]: https://www.assemblyscript.org/
[as-pect]: https://www.npmjs.com/package/@as-pect/cli

# NEAR-AS-Boilerplate

```javascript
import { Context, logging, storage } from "near-sdk-as";
```

`Context ` - This object provides context for contract execution including information about the transaction sender, blockchain height, and attached deposit available for use during contract execution, etc. The snippet below is the complete interface as currently implemented.

`logging` - append to the execution environment log (appears in JS Developer Console when using near-api-js)

`storage` - // key-value store for the contract (used by PersistentMap, PersistentVector and PersistentDeque)

```javascript
export function getGreeting(accountId: string): string | null {
  return storage.get < string > (accountId, DEFAULT_MESSAGE);
}
```

This function simply returns a value if the key defined by `accountId` exists. If it does not, then `DEFAULT_MESSAGE` will be returned instead

```javascript
export function setGreeting(message: string): void {
  const account_id = Context.sender;

  // Use logging.log to record logs permanently to the blockchain!
  logging.log(
    'Saving greeting "' + message + '" for account "' + account_id + '"'
  );

  storage.set(account_id, message);
}
```

this will set a string value ot the key of `account_id`. `Context.sender` will return the account ID string that signed the original transaction that led to this execution
