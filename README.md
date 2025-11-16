# bluefin-common

Shared OCI layer containing common configuration files used across all Bluefin variants (bluefin, bluefin-dx, bluefin-lts).

## What's Inside

This layer contains two main configuration directories:

### `/etc/ublue-os/` - System Configuration
- **Bling configuration** - CLI theming settings
- **Fastfetch settings** - System information display configuration
- **Setup configuration** - First-boot and system setup parameters

### `/usr/share/ublue-os/` - User-Space Configuration
- **Firefox defaults** - Pre-configured Firefox settings
- **Flatpak overrides** - Application-specific Flatpak configurations
- **Just recipes** - Additional command recipes for system management
- **MOTD templates** - Message of the day and tips
- **Setup hooks** - Scripts for privileged, system, and user setup stages

## Usage in Containerfile

Reference this layer as a build stage and copy the directories you need:

### Copy everything:
```dockerfile
FROM ghcr.io/ublue-os/bluefin-common:latest AS bluefin-common

# Copy all system files
COPY --from=bluefin-common /system_files /
```

### Copy only system configuration:
```dockerfile
FROM ghcr.io/ublue-os/bluefin-common:latest AS bluefin-common

# Copy only /etc configuration
COPY --from=bluefin-common /system_files/etc /etc
```

### Copy only user-space configuration:
```dockerfile
FROM ghcr.io/ublue-os/bluefin-common:latest AS bluefin-common

# Copy only /usr/share configuration
COPY --from=bluefin-common /system_files/usr /usr
```

## Building Locally

```bash
just build
```

## Contributing

See [AGENTS.md](AGENTS.md) for development guidelines and instructions.

## TODO

Split this repo into common and bluefin specific so Aurora can copy out what is image agnostic, that way we can share config. 
