# nixfiles-builder

Builds and publishes NixOS system configurations to an Attic cache.

In this GitHub repository, open **Settings → Secrets and variables → Actions**
and add these repository secrets.

| Secret | Value |
| --- | --- |
| `ATTIC_ENDPOINT` | The Attic server's HTTPS API base URL, such as `https://cache.example.com/`. |
| `ATTIC_TOKEN` | An Attic API token with pull and push access to the target cache. |
| `ATTIC_CACHE` | The exact name of the existing Attic cache to publish to. |