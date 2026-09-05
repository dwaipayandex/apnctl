# apnctl

**APN control for the Nokia AOD311NK** (Airtel AirFiber ODU) — a small compiled CLI that logs into the router's web interface and changes the cellular APN without opening the browser UI.

Distributed as a prebuilt binary only.

- Supported device: Nokia AOD311NK (5G32-A), FW AOD311NK_R_1.0 / web build 2402.20.06.A17
- Current package: macOS Apple Silicon (arm64) executable
- No installation required — download `apnctl`, make it executable, run it

> For use on hardware you own. The tool performs only the same APN read/write
> operations available in the device's own web UI.

## Quick start

```sh
chmod +x apnctl

# 1. Check what's configured now
APNCTL_PASSWORD=<router password> ./apnctl apn get

# 2. Change the APN (example: BSNL)
APNCTL_PASSWORD=<router password> ./apnctl apn set bsnlnet

# 3. Check the router connection state
APNCTL_PASSWORD=<router password> ./apnctl status
```

The router ships with the web password set to the device serial number
(printed on the label), unless it was changed.

## Commands

| Command | Effect |
|---|---|
| `login` | authenticate and show session info |
| `apn get` | list configured APN instances and their state |
| `apn set <name>` | switch the APN (instance 1) to `<name>` and verify |
| `apn set <name> -i <N>` | switch APN instance `N` |
| `status` | dump the current connection status |

## Options

```
-H <url>        router base url (default https://192.168.0.1)
-u <user>       web account (default admin)
-p <password>   web password (else $APNCTL_PASSWORD, else prompt)
-k              enable TLS verification (off by default: self-signed cert)
-t <seconds>    per-request timeout (default 15)
-v              verbose output
```

## Notes

- The APN change survives a reboot. A factory reset on the device restores
  the original APN and password.
- After an APN change it can take a minute for the modem to re-register and
  for data to flow; `status` shows when the connection is back up.
- Bug reports and feature requests: open an issue.

## Integrity

SHA-256 of `apnctl`:

```
ae650913b483679493850ebd040bfbd2761be440161f6b553ddb22224e15812f
```
