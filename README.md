# Useful podman containers
This directory is to be setup inside `~/.containers` directory

# Prerequisites
## Required packages
`podman` and `podman-compose` is required:
```
$ sudo pacman -S podman podman-compose
```

## Allow traffic for required ports
Assuming `ufw` is the setup firewall use following commands to allowlist required ports for mentioned application.

### Jellyfin required ports
```
$ sudo ufw allow 8096/tcp comment "Allow Jellyfin Web UI"
$ sudo ufw allow 1900/udp comment "Allow Jellyfin DLNA Discovery"
$ sudo ufw allow 7359/udp comment "Allow Jellyfin Auto-discovery"
```

# Start and shutdown containers
To start the containers with pwd set as directory containing `compose.yaml` use this command:
```
$ podman-compose up -d
```

To start the containers with any pwd:
```
$ podman-compose -f <path-to-compose.yaml> up -d
```

To stop the containers mentioned in a `compose.yaml`:
```
$ podman-compose down
```

# Nvidia support
Nvidia hardware decoding support from podman requires a separate package `nvidia-container-toolkit`:
```
$ sudo pacman -S nvidia-container-toolkit
```

Generate the CDI Specification: Podman relies on the Container Device Interface (CDI) specification to map the GPU into the container. You must generate this file, typically with a command like:
```
$ sudo nvidia-ctk cdi generate --output=/etc/cdi/nvidia.yaml
```
