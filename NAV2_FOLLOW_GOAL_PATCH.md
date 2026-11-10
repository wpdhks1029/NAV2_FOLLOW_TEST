# Follower RViz goal pursuit patch

Branch: `nav2-follow-goal-pursuit`

On Ubuntu, clone this branch and reassemble the follower-only patch:

```bash
git clone --branch nav2-follow-goal-pursuit https://github.com/wpdhks1029/NAV2_FOLLOW_TEST.git ~/nav2_follow_goal_pursuit
cd ~/nav2_follow_goal_pursuit
cat nav2-follow-goal-deployment.tar.gz.b64.part* | base64 -d > nav2-follow-goal-deployment.tar.gz
sha256sum nav2-follow-goal-deployment.tar.gz
```

Expected SHA-256: `14812341f6f7e2795427090d4c8e4f8e77d135dc04f1bb49d6ead643fe4b58f7`.

The archive contains six files for `~/nav2_follow_integration/baseline/follower_diagnostics`. Back up those destination files before overlaying. Use the standard 360 second local-avoidance hardware driver without `--ack-continuous20-candidate`. Launch the follower follow-only process before setting a new RViz 2D Goal Pose. It auto-arms only after an active NavigateToPose goal, fresh plan, graph, motor feedback, map pose and scan pass preflight. Each run handles one goal and stops on goal terminal status or safety failure. This is offline-verified code; it has not been physically validated.
