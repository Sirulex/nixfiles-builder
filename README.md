<img src="assets/icon.svg" width="64" height="64" alt="">

# nixfiles-builder

## Flyline binary cache

The [Flyline workflow](.github/workflows/flyline.yml) checks the upstream default
branch at the start of every hour (UTC). It uses the upstream `flake.lock` and
checks the resulting store path in Attic for `x86_64-linux` and `aarch64-linux`.
It builds and uploads a package only when its store path is missing from the cache.

In this GitHub repository, open **Settings → Secrets and variables → Actions**
and add these repository secrets.

| Secret | Value |
| --- | --- |
| `ATTIC_ENDPOINT` | The Attic server's HTTPS API base URL, such as `https://cache.example.com/`. |
| `ATTIC_TOKEN` | An Attic API token with pull and push access to the target cache. |
| `ATTIC_CACHE` | The exact name of the existing Attic cache to publish to. |

All three secrets are required. The workflow checks the settings and verifies
pull and push access before installing Nix.

Once the workflow is on the default branch, select **Actions → Build and cache
Flyline → Run workflow** to run it on demand.

GitHub disables scheduled workflows in public repositories after 60 days of
repository inactivity. You can re-enable the workflow from the **Actions** tab.
[GitHub schedule documentation](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#schedule)
