# Voicebox

Built from the upstream release tag by `.github/workflows/publish-voicebox.yaml`,
using upstream's own Dockerfile. There is no local Dockerfile.

- `ghcr.io/chocolateandmilkwin/voicebox:<version>-cpu` (GitHub) and
  `forgejo.nsns.dk/chocolateandmilkwin/voicebox:<version>-cpu` (Forgejo, `.forgejo/workflows/publish-voicebox.yaml`):
  arm64, PyTorch CPU (radxa nodes)

To update, change `VOICEBOX_VERSION` in both workflows. The container listens on port 17493.
