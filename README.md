# Nav2 + follower isolated experiment

This branch contains the isolated deployment bundle. The previous successful backup remains unchanged.

Reassemble on Ubuntu after pulling this branch:

    cat nav2-follow-deployment.tar.gz.b64.part* | base64 -d > nav2-follow-deployment.tar.gz
    sha256sum nav2-follow-deployment.tar.gz
    tar -xzf nav2-follow-deployment.tar.gz

Expected SHA-256: 16b1b3b5ffb405666113f77a31fe9fb7f5a49b34d37f3cd847c142d346283ee7.

The extracted tree is baseline/follower_diagnostics. Logs were omitted except the saved new-map reference. See the included README for verification scope and runtime cautions.