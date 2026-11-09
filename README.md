# Nav2 + follower isolated experiment

This branch contains the experimental deployment bundle as three base64 text parts.

Reassemble on Ubuntu after cloning or pulling this branch:

```bash
cat nav2-follow-deployment.tar.gz.b64.part* | base64 -d > nav2-follow-deployment.tar.gz
sha256sum nav2-follow-deployment.tar.gz
tar -xzf nav2-follow-deployment.tar.gz
```

Expected SHA-256: `43440f61d88e29a7d26eb6b80b17f7ee8939f0287d405ca709943e4db3d9e296`.

The extracted tree is `baseline/follower_diagnostics`. Logs were omitted except the saved new-map reference `logs/new_map_reference_20261107.json`. The successful backup was not modified. See `baseline/follower_diagnostics/README.md` for virtual verification scope and runtime cautions.
