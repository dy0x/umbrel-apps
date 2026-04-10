# dy0x's Umbrel App Store

A community app store for [Umbrel](https://umbrel.com) featuring self-hosted Bitcoin, Monero and privacy apps.

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
- Default username: `abc`
- Default password: `bisq`
- Data is persisted across restarts

### XMR Mempool
- Connects directly to your Umbrel Monero node via RPC — no third-party node required
- Requires the [Monero](https://apps.umbrel.com/app/monero) app to be installed on your Umbrel
