# luci-app-tailscale-community

LuCI web interface for managing [Tailscale](https://tailscale.com) on OpenWrt.

This repo is a **build mirror** of the upstream `luci-app-tailscale`, synced automatically and built via GitHub Actions. Packages are published in both formats:

| OpenWrt version | Package format | Package manager |
|---|---|---|
| 24.10 and older | `.ipk` | `opkg` |
| 25.12 and newer / snapshot | `.apk` | `apk` |

> The package is architecture-independent (pure LuCI), so one file works on any target (x86_64, aarch64, mipsel, bcm27xx, etc.). You still need the `tailscale` package itself installed.

## Features

- Manage Tailscale from LuCI (**Services → Tailscale**)
- Login / logout and connection status
- Configure routes, exit node, and other Tailscale options from the web UI
- Multi-language support (`po/`)

## Installation

Download the latest package from the [Releases](../../releases) page.

### OpenWrt 24.10 and older (`.ipk`)

```sh
opkg update
opkg install tailscale
opkg install /tmp/luci-app-tailscale-community_*.ipk
```

### OpenWrt 25.12 and newer / snapshot (`.apk`)

```sh
apk update
apk add tailscale
apk add --allow-untrusted /tmp/luci-app-tailscale-community-*.apk
```

Then refresh LuCI:

```sh
rm -rf /tmp/luci-indexcache* /tmp/luci-modulecache
/etc/init.d/uhttpd restart
```

Open **Services → Tailscale** in LuCI.

## Build

Builds run through GitHub Actions (`.github/workflows`):

- **Trigger:** `workflow_dispatch` (manual)
- **Output:** `.ipk` and `.apk` uploaded to GitHub Releases
- **SDK used:**
  - `.ipk`: OpenWrt 24.10 SDK (x86/64)
  - `.apk`: OpenWrt snapshot SDK (x86/64)

### Manual build with the SDK

```sh
# inside the OpenWrt SDK directory
git clone https://github.com/Yogxx/luci-app-tailscale-community package/luci-app-tailscale-community
make defconfig
make package/luci-app-tailscale-community/compile V=s
```

## Upstream sync

Source is synced automatically from the upstream `luci-app-tailscale` repo. Local customizations (e.g. the menu path `admin/services/tailscale`) are preserved across syncs.

## Credits

- Original LuCI app: upstream `luci-app-tailscale` authors
- [Tailscale](https://tailscale.com)
- Build mirror & packaging: [@Yogxx](https://github.com/Yogxx)

## License

Same as upstream. See the upstream repository for details.
