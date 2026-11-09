# Nav2 + follower isolated experiment

This branch contains the experimental deployment bundle as three base64 text parts.

Reassemble on Ubuntu after cloning or pulling this branch:

```bash
cat nav2-follow-deployment.tar.gz.b64.part* | base64 -d > nav2-follow-deployment.tar.gz
sha256sum nav2-follow-deployment.tar.gz
tar -xzf nav2-follow-deployment.tar.gz
```

Expected SHA-256: `a77badc14db0f4a09e8218fdeed97c47a3cafbbe9c092a3a8bfe655429a3eb4b`.

The extracted tree is `baseline/follower_diagnostics`. Logs were omitted except the saved new-map reference `logs/new_map_reference_20261107.json`. The successful backup was not modified. See `baseline/follower_diagnostics/README.md` for virtual verification scope and runtime cautions.
