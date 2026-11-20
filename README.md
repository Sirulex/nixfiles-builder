# nixfiles-builder

Builds and publishes NixOS system configurations to an Attic cache.

The [Flyline workflow](.github/workflows/flyline.yml) runs at the start of every
hour (UTC). Each run locks the latest upstream Flyline revision and the current
Nixpkgs tarball from the `nixos-unstable` channel. Flyline follows that Nixpkgs
input, as it does in Nixfiles. The builder checks Attic and builds and uploads
any missing Flyline packages for `x86_64-linux` and `aarch64-linux`.

Nixfiles can use the cached package once its `flake.lock` pins the same two
revisions. The builder keeps its lock file on the runner for the duration of the
job.

In this GitHub repository, open **Settings → Secrets and variables → Actions**
and add these repository secrets.

| Secret | Value |
| --- | --- |
| `ATTIC_ENDPOINT` | The Attic server's HTTPS API base URL, such as `https://cache.example.com/`. |
| `ATTIC_TOKEN` | An Attic API token with pull and push access to the target cache. |
| `ATTIC_CACHE` | The exact name of the existing Attic cache to publish to. |

The workflow requires all three secrets and verifies Attic access before
installing Nix.
