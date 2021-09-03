# podman-desktop

podman runs on linux, so this script spins up a virtual linux machine, and configures podman to use it as a remote host.

<img width="907" alt="Screen Shot 2021-09-03 at 11 22 37 AM" src="https://user-images.githubusercontent.com/32407/132029535-20ab9aac-6c8d-440e-9122-660363e7f10a.png">

Requires `muiltipass` and `podman`

> if you are on Apple Silicon, use multipass [1.8.0](https://multipass-ci.s3.amazonaws.com/pr403/multipass-1.8.0-dev.403.pr403%2Bg843f3ca3.mac%2Barm64-Darwin.pkg)

    brew install multipass podman

Setup a vm for podman. Values shown here are defaults. Mounts are the same as Docker Desktop.

    podman-desktop \
      --name podman \
      --identity ~/.ssh/id_rsa \
      --cpus 2 \
      --mem 2G \
      --disk 10G \
      20.04

If you'd like to pass any other params to `multipass launch`, just put them after `--`

    podman-desktop -- --network <spec>

If you'd like to change the default mounts, set the `MOUNTS` variable to an array
