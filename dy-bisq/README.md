<p align="center">
  <img src="icon.png" alt="Bisq Logo" width="21%">
</p>

# Bisq on Umbrel

> **Upstream docs:** <https://bisq.wiki/>
>
> Everything not listed in this document should behave the same as upstream
> Bisq. If a feature, setting, or behavior is not mentioned here, the upstream
> documentation is accurate and fully applicable.

[Bisq](https://bisq.network/) is a decentralized peer-to-peer Bitcoin exchange. Trade Bitcoin for fiat currencies and other cryptocurrencies without intermediaries, KYC, or centralized servers.

---

## Architecture

| Property      | Value                                                                 |
|---------------|-----------------------------------------------------------------------|
| Image source  | Custom multi-stage Dockerfile (Ubuntu Jammy builder + KasmVNC Debian Bookworm webtop, flattened via `FROM scratch`) |
| Architectures | x86_64 only                                                          |
| Entrypoint    | `unshare --pid --fork --mount-proc /init` (s6-overlay requires PID 1 in its own namespace) |

Bisq is a JavaFX desktop application with no web interface. This package runs it inside a browser-accessible Linux desktop (webtop) powered by KasmVNC:

```
Browser -> KasmVNC (port 3000) -> Openbox -> Bisq (JavaFX)
```

## Volume and Data Layout

| Volume | Mount point | Contents                                                  |
|--------|-------------|-----------------------------------------------------------|
| `${APP_DATA_DIR}/data` | `/config`   | Webtop home, Bisq application data         |

- **`/config/.local/share/Bisq/`** — upstream Bisq data directory (wallet, trades, settings)
- **`/config/.local/share/Bisq/bisq.properties`** — generated at launch by `startwm.sh`

## Configuration Management

The `bisq.properties` file is regenerated on every launch by `startwm.sh` with:
- `useTorForBtc=false` 
- Empty banned node lists

## Network Access and Interfaces

| Interface      | Port | Protocol | Purpose                         |
|----------------|------|----------|---------------------------------|
| Bisq Desktop   | 3000 | HTTP     | KasmVNC web interface (full Bisq desktop in browser) |

Umbrel maps this internally through its `app_proxy` service, making the application available over the Umbrel dashboard securely. A default password (`bisq`) is set to bypass the KasmVNC authentication prompt, as Umbrel handles authentication.

## Dependencies

| Dependency       | Required | Purpose                    |
|------------------|----------|----------------------------|
| Bitcoin (`bitcoin`) | Yes  | Blockchain data            |

## Limitations and Differences

1. **x86_64 only** — Bisq does not provide official ARM builds.
2. **No direct desktop access** — Bisq runs inside a KasmVNC webtop, not as a native desktop app.
3. **`bisq.properties` is overwritten on every start** — manual edits to this file will not persist.
4. **First launch is slow** — Bisq needs to connect to the P2P trading network and sync, which can take several minutes.

## What Is Unchanged from Upstream

- All trading functionality (offers, trades, disputes)
- Wallet management (send, receive, backup seed)
- All Bisq UI settings and preferences
- P2P network participation
- DAO functionality

## Development Testing on Umbrel

If you are developing this app using the Umbrel developer environment:

1. Clone this repository into your `umbrel-dev/apps` folder.
2. Run `docker compose up -d` within this repository or use `umbrel app install bisq`.
3. The Dockerfile will locally build, combining the Bisq application with KasmVNC to create the web-ready output.
