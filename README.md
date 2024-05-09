# github-action-build-dockerfile

## Description

Cache aware building of Dockerfiles.

## Inputs

| name | description | required | default |
| --- | --- | --- | --- |
| `args` | <p>Newline separated build arguments, e.g. "VERSION=foo\nAUTHOR=bar".</p> | `false` | `""` |
| `cache_refs` | <p>JSON array of refs which will trigger publishing layers to gha cache. Use long lived branches.</p> | `false` | `["refs/heads/main", "refs/heads/master"]` |
| `context` | <p>Docker build context directory. Defaults to "Git context" so you don't need to use actions/checkout, but it will not pickup local changes. Point to a directory to pickup local changes from a checkout, e.g. '.' or './alt/docker/build/path'.</p> | `false` | `{{defaultContext}}:.` |
| `file` | <p>Dockerfile path (relative to build context).</p> | `false` | `Dockerfile` |
| `image` | <p>Image name.</p> | `false` | `${{ github.repository }}` |
| `platforms` | <p>target platforms to build image(s) for, e.g. 'linux/amd64,linux/arm64'.</p> | `false` | `linux/amd64` |
| `push` | <p>The string 'true' to push the built image to registry, otherwise the string 'false'.</p> | `false` | `false` |
| `registry` | <p>Registry to publish to.</p> | `false` | `ghcr.io` |
| `registry_username` | <p>Username</p> | `false` | `${{ github.actor }}` |
| `registry_token` | <p>Password</p> | `true` | `""` |
| `secrets` | <p>Newline separated build secrets, e.g. "VERSION=foo\nAUTHOR=bar".</p> | `false` | `""` |
| `target` | <p>Target stage to build</p> | `false` | `""` |


## Outputs

| name | description |
| --- | --- |
| `image_digest` | <p>Image Digest</p> |
| `image_name` | <p>Image Name</p> |
| `metadata` | <p>Docker Metadata</p> |
