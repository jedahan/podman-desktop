# podman-desktop

podman runs on linux, so this script spins up a virtual linux machine, and configures podman to use it as a remote host.

<img width="907" alt="Screen Shot 2021-09-03 at 11 22 37 AM" src="https://user-images.githubusercontent.com/32407/132029535-20ab9aac-6c8d-440e-9122-660363e7f10a.png">

Requires `muiltipass` and `podman`

    brew install multipass podman

Setup a vm for podman. Values shown here are defaults. Mounts are the same as Docker Desktop.

    podman-desktop \
      --name podman \
      --identity ~/.ssh/podman \
      20.04

If you'd like to pass any other params to `multipass launch`, just put them after `--`

    podman-desktop -- --cpus 3  --mem 3G --network <spec>

If you'd like to change the default mounts, set the `MOUNTS` variable to an array
