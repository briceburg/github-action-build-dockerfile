# github-action-build-dockerfile

Cache aware building and publishing of Dockerfiles.

## Usage

Works well with [github-action-detect-image-metadata](https://github.com/briceburg/github-action-detect-image-metadata) to set the image labels and tags.

```yaml
jobs:
  build-dockerfile:
    runs-on: ubuntu-latest
    steps:
    - id: meta
      uses: briceburg/github-action-detect-image-metadata
    - uses: briceburg/github-action-build-dockerfile
      with:
        image-labels: ${{ steps.meta.outputs.labels }}
        images: ${{ steps.meta.outputs.images }}
        push: 'true'
```

## Inputs

| name | description | required | default |
| --- | --- | --- | --- |
| `build-args` | <p>Newline separated build arguments, e.g. "VERSION=foo\nAUTHOR=bar".</p> | `false` | `""` |
| `build-secrets` | <p>Newline separated build secrets, e.g. "VERSION=foo\nAUTHOR=bar".</p> | `false` | `""` |
| `build-target` | <p>Target stage to build</p> | `false` | `""` |
| `cache-branches` | <p>JSON array of branches which trigger publishing layers to gha cache. Use long lived branches. E.g. '["main", "master"]'. If empty, uses the default branch.</p> | `false` | `["${{ github.event.repository.default_branch }}"]` |
| `context` | <p>Docker build context directory. Defaults to "Git context" so you don't need to use actions/checkout, but it will not pickup local changes. Point to a directory to pickup local changes from a checkout, e.g. '.' or './alt/docker/build/path'.</p> | `false` | `{{defaultContext}}:.` |
| `dockerfile-path` | <p>Dockerfile path (relative to build context).</p> | `false` | `Dockerfile` |
| `image-labels` | <p>Newline list of Image Labels (in name=value format)</p> | `false` | `""` |
| `images` | <p>Newline list of images (in registry/image-name:tag format)</p> | `false` | `""` |
| `platforms` | <p>target platforms to build image(s) for, e.g. 'linux/amd64,linux/arm64'.</p> | `false` | `linux/amd64` |
| `push` | <p>The string 'true' to push the built image to registry, otherwise the string 'false'.</p> | `false` | `true` |
| `skip-summary` | <p>The string 'true' to skip writing the job summary, otherwise the string 'false'.</p> | `false` | `false` |

## Outputs

| name | description |
| --- | --- |
| `image-digest` | <p>Image Digest</p> |

In addition to the action outputs, the following environment variables are set:

| name | description |
| --- | --- |
| `BUILD_DOCKERFILE_IMAGE_DIGEST` | <p>Image Digest</p> |

