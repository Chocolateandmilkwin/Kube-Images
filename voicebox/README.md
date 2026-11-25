# Voicebox

Built from the upstream release tag by `.github/workflows/publish-voicebox.yaml`,
using upstream's own Dockerfile. There is no local Dockerfile.

- `ghcr.io/chocolateandmilkwin/voicebox:<version>-cpu`: arm64, PyTorch CPU (radxa nodes)

To update, change `VOICEBOX_VERSION` in the workflow. The container listens on port 17493.
