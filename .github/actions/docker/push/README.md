# Docker Push
Action: [apply](./action.yml)

This action pushes a docker image to a registry.

## Inputs
| Name               | Description                  | Required | Default Value |
|--------------------|------------------------------|----------|---------------|
| `image-identifier` | The image identifier to push | false    | N/A           |

## Example
```yaml
jobs:
  apply:
    name: Push docker image
    runs-on: ubuntu-latest
    steps:
      - name: Build
        uses: cupel-co/actions/.github/actions/docker/push@vx.x.x
        with:
          image-identifier: 'cupel-co/api' 
```
