# ComfyUI ROCm image

This image runs ComfyUI v0.28.0 with the AMD ROCm PyTorch nightly for
`gfx1151`, the GPU architecture in the Ryzen AI Max+ 395 on `nc13`.
It installs ComfyUI-Manager 4.2.1 or newer.

## Models

The image does not contain models. Model checkpoints, VAEs, LoRAs, and other
weights are downloaded separately through ComfyUI-Manager or copied into
`/workspace/ComfyUI/models` at runtime. Mount a persistent volume at that path
in the Kubernetes Deployment so downloads survive pod replacement and do not
increase image build or pull time.

The Forgejo workflow publishes:

```text
forgejo.nsns.dk/chocolateandmilkwin/comfy-ui:latest
forgejo.nsns.dk/chocolateandmilkwin/comfy-ui:sha-<commit>
```

Before its first run, configure these repository Action secrets:

- `REGISTRY_USERNAME`: the Forgejo account that owns a package-write token.
- `REGISTRY_TOKEN`: a Forgejo personal access token with the `write:package`
  scope.

To let Kubernetes pull the private image, create a registry secret in the
`ai` namespace using an account or token with `read:package`:

```sh
kubectl -n ai create secret docker-registry forgejo-registry \
  --docker-server=forgejo.nsns.dk \
  --docker-username='<forgejo-user>' \
  --docker-password='<forgejo-token>'
```

Reference `forgejo-registry` in the ComfyUI Deployment's `imagePullSecrets`
and set the image to
`forgejo.nsns.dk/chocolateandmilkwin/comfy-ui:sha-<commit>`.
