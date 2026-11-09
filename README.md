# Nav2 + follower isolated experiment

This branch contains the isolated deployment bundle. The previous successful backup remains unchanged.

Reassemble on Ubuntu after pulling this branch:

    cat nav2-follow-deployment.tar.gz.b64.part* | base64 -d > nav2-follow-deployment.tar.gz
    sha256sum nav2-follow-deployment.tar.gz
    tar -xzf nav2-follow-deployment.tar.gz

Expected SHA-256: d100eb03c473bc5cfdee2f75cbcbb3f0bb6413ea9b6a3322b100e439f37a7cc7.

The extracted tree is baseline/follower_diagnostics. Logs were omitted except the saved new-map reference. See the included README for verification scope and runtime cautions.