# Nav2 + follower isolated experiment

This branch contains the experimental deployment bundle as three base64 text parts because the GitHub connector does not upload binary files directly.

Reassemble on Ubuntu after cloning this branch:

```bash
cat nav2-follow-deployment.tar.gz.b64.part* | base64 -d > nav2-follow-deployment.tar.gz
sha256sum nav2-follow-deployment.tar.gz
tar -xzf nav2-follow-deployment.tar.gz
```

Expected SHA-256: `29a24cc54a6c2f2aa1c41b837274c1e37ade273d5a0ecf865a9cc5f3f45a054d`.

The extracted tree is `baseline/follower_diagnostics`. Logs were omitted except the saved new-map reference `logs/new_map_reference_20261107.json`. The existing successful backup was not modified. See the original experiment README at the branch root for virtual verification scope and runtime cautions.
