# ZEIT ONLINE Image signing action

---

**_NOTE:_** This Action is used internally by the ZEIT ONLINE organization and is probably not useful outside of this specific context.

---

## Summary

This composite action install the `cosign` CLI tool and uses it to sign images. It is up to the user to provide authentication to the
relecant registry, if needed. In ZEIT ONLINE building workflows this is provided by the [Baseproject action](https://github.com/ZeitOnline/gh-action-baseproject/).

## Example Usage

```yaml
jobs:
    build:
        # ...
        steps:
            # ...
            - name: Sign Image
              uses: ZeitOnline/sign-image-action@v1.0.1
              with:
                image_name: ${{ env.PROJECT }}
                digest: ${{ steps.push.outputs.digest }}
            # ...
```

This usage assumes a preceding step with id `push` that outputs the digest of the Docker image that was pushed to a registry. This
can, for example, be done with the official action `docker/build-push-action`.

## Reference

Here are all the inputs available through `with`:

| Input                | Description                                                                       | Default | Required |
| -------------------- | --------------------------------------------------------------------------------- | ------- | -------- |
| `repository`       | The name of the repository where the image is hosted | `europe-west3-docker.pkg.dev/zeitonline-engineering/docker-zon`        | ✔        |
| `image_name`        | The name of the image to be signed                                        |         | ✔        |
| `digest`          | The digest of the image to be signed                                              |         |    ✔      |

## Releases

This action uses [Release Please](https://github.com/googleapis/release-please-action). To create a new release, create a PR and use [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) as described [here](https://docs.zeit.de/ops/terraform-infra/terraform/repos.html#modulversionierung).
