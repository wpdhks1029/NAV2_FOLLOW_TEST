# Nav2 + follower isolated experiment

This branch contains the experimental deployment bundle as three base64 text parts.

Reassemble on Ubuntu after cloning or pulling this branch:

```bash
cat nav2-follow-deployment.tar.gz.b64.part* | base64 -d > nav2-follow-deployment.tar.gz
sha256sum nav2-follow-deployment.tar.gz
tar -xzf nav2-follow-deployment.tar.gz
```

Expected SHA-256: `8f8c72a2e7d1b218bff33c6ec33db38404fb73ee0509c95f6286d2f8f307ac07`.

The extracted tree is `baseline/follower_diagnostics`. Logs were omitted except the saved new-map reference `logs/new_map_reference_20261107.json`. The successful backup was not modified. See `baseline/follower_diagnostics/README.md` for virtual verification scope and runtime cautions.
