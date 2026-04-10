# dy0x's Umbrel App Store

A community app store for [Umbrel](https://umbrel.com) featuring self-hosted Bitcoin and privacy apps.

## Apps

| App | Description | Version |
|-----|-------------|---------|
| [Bisq](dy-bisq/) | Decentralized peer-to-peer Bitcoin exchange — trade Bitcoin for fiat without KYC or intermediaries | 1.9.22 |
| [XMR Mempool](dy-xmr-mempool/) | Self-hosted Monero mempool explorer — browse pending transactions, fee estimates, and block history | 1.0.0 |

## Add to Umbrel

In your Umbrel dashboard go to **App Store → Community App Stores** and add:

```
https://github.com/dy0x/umbrel-apps
```

## Notes

### Bisq
- Runs as a full desktop app inside a browser-accessible KasmVNC session
- Default password: `bisq`
- Data is persisted across restarts

### XMR Mempool
- Connects to a Monero node via RPC — defaults to a public node (`xmr-node.cakewallet.com`)
- To use your own node, set `MONERO_NODE_1_HOST`, `MONERO_NODE_1_PORT`, and `MONERO_NODE_1_TLS` environment variables
