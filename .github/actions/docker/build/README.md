# Docker Build
Action: [build](./action.yml)

The Docker Build GitHub Action builds a Docker image using the provided Dockerfile and tags it with the specified tag.

## Inputs
| Name                | Description                                | Required | Default Value |
|---------------------|--------------------------------------------|----------|---------------|
| `arguments`         | Additional arguments for the build command | false    | N/A           |
| `dockerfile`        | The dockerfile to build                    | true     | `Dockerfile`  |
| `name`              | The name of the image                      | true     | N/A           |
| `tag`               | The tag of the image                       | true     | N/A           |
| `target`            | The target to build                        | true     | N/A           |
| `working-directory` | Directory that contains the dockerfile     | true     | `./`          |

## Outputs
| Name               | Description          |
|--------------------|----------------------|
| `image-identifier` | The image identifier |

## Example
```yaml
jobs:
  apply:
    name: Build dockerfile
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
          fetch-tags: true
      - name: Build
        uses: cupel-co/actions/.github/actions/docker/build@vx.x.x
        with:
          arguments: '--build-arg VERSION=1.0.0'
          dockerfile: 'Dockerfile'
          name: 'api'
          tag: 'v1.0.0'
          target: 'api'
          working-directory: './'  
```
