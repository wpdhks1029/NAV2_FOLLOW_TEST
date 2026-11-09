# Nav2 + follower isolated experiment

This branch contains the isolated deployment bundle. The previous successful backup remains unchanged.

Reassemble on Ubuntu after pulling this branch:

    cat nav2-follow-deployment.tar.gz.b64.part* | base64 -d > nav2-follow-deployment.tar.gz
    sha256sum nav2-follow-deployment.tar.gz
    tar -xzf nav2-follow-deployment.tar.gz

Expected SHA-256: 9cd460aaaeb2b6071855c35e4b98a8354aab66cea7b9e20c8059c8a974be2106.

The extracted tree is baseline/follower_diagnostics. Logs were omitted except the saved new-map reference. See the included README for verification scope and runtime cautions.