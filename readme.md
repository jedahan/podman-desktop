# podman-desktop

podman runs on linux, so this script spins up a virtual linux machine, and configures podman to use it as a remote host.

Requires `muiltipass` and `podman`

> if you are on Apple Silicon, use multipass [1.8.0](https://multipass-ci.s3.amazonaws.com/pr403/multipass-1.8.0-dev.403.pr403%2Bg843f3ca3.mac%2Barm64-Darwin.pkg)

    brew install multipass podman

Setup a vm for podman. Values shown here are defaults. Mounts are the same as Docker Desktop.

    INSTANCE_NAME="podman" \
    VERSION_ID="20.04" \
    IDENTITY="~/.ssh/id_rsa" \
    PUBKEYFILE="$IDENTITY.pub" \
    MOUNTS="/Users /Volumes /private /tmp /var/folders" \
      podman-desktop
