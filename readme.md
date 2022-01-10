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

By default, podman-desktop will mount the same folders as Docker Desktop.

If you'd like to change the default mounts, set the `MOUNTS` variable to an array

If you'd like to mount nothing, (for example, due to sshfs_server cpu usage) set `MOUNTS` to an empty string.


## Image building with buildkit

Podman builds are considerably slower compared to Docker builds. One way to mitigate this is to use [buildkit](https://github.com/moby/buildkit). Multipass instances provisioned with podman-desktop already contain a ready-to-go buildkit daemon. All you need to do is use the buildkit-cli from your host system:

	buildctl \
		--addr=tcp://$(shell multipass info podman --format json | jq -r ".info.podman.ipv4[]"):1234 \
		build \
		--frontend dockerfile.v0 \
		--local context=. \
		--local dockerfile=. \
		--output type=oci,name="thisgetsignored:imagename" \                                                                                               
		| podman load
	

Please note, the resulting image will be `localhost/imagename:latest`, because [Buildkit does not seem write OCI compliant image annotations](https://github.com/containers/podman/issues/12560#issuecomment-990826349-permalink).
