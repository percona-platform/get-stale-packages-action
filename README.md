# get-stale-packages-action

## Usage

This action queries repository packages using a token from the `ROBOT_TOKEN` environment variable
and sets the` STALE_VERSIONS` environment variable with a list of package IDs that
were built more than one week ago and should be removed as stale.

It typically should be used by "Clean" workflow (in .github/workflows/clean.yml file)
in the "clean-packages" job with the following steps:

```yaml
- name: Collect stale package versions
  env:
    ROBOT_TOKEN: ${{ secrets.ROBOT_TOKEN }}
  uses: percona-platform/get-stale-packages-action@v1.0.0

- name: Clean stale packages
  if: env.STALE_VERSIONS
  uses: percona-platform/delete-package-versions@v1.0.3
  with:
    package-version-ids: ${{ env.STALE_VERSIONS }}
```
