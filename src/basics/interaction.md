# Program interaction

Continuing with our example program, [GraffitiWall], we find an implementation example of how to communicate with a deployed [program] by looking at the frontend code; specifically, we'll look at the [CreateArchAccount.tsx] file.

Inside this file we initialize a new instance of RPC client, construct, sign and send a few transactions, and then poll the network for the processed transaction results.

After receiving the relayed instructions from the RPC server, the Arch Network [validator] nodes will execute the program logic within the context of the Arch VM, signing-off on the execution and then pass the results to the [leader] who will ultimately submit a signed Bitcoin transaction back to the Bitcoin network.

Let's go through it line-by-line.

Here we'll initialize a new Arch RPC client and pass in the URL, otherwise we'll default to a service running on our localhost. 
```ts
const client = new ArchRpcClient((import.meta as any).env.VITE_ARCH_NODE_URL || 'http://localhost:9002');
```

Next, you'll find the class `GraffitiMessage`, which will mirror the data structure that we use within our [GraffitiWall] program.
```ts
// CreateArchAccount.tsx
class GraffitiMessage {
  constructor(
    public timestamp: number,
    public name: string,
    public message: string
  ) {}
}
```

And here's the data structure found in our `src/app/program/src/lib.rs`.
```rust,ignore
#[derive(Debug, Clone, BorshSerialize, BorshDeserialize)]
pub struct GraffitiMessage {
    pub timestamp: i64,
    pub name: [u8; 16],
    pub message: [u8; 64],
}
```

[leader]: ../concepts/nodes.md
[program]: ../program/program.md
[validator]: ../concepts/nodes.md
[GraffitiWall]: https://github.com/Arch-Network/arch-cli/blob/main/src/app/program/src/lib.rs
[CreateArchAccount.tsx]: https://github.com/Arch-Network/arch-cli/blob/main/src/app/frontend/src/components/CreateArchAccount.tsx

