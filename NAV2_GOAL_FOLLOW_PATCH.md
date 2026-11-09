# RViz 2D Goal follower patch

This archive adds the isolated Nav2 plan source for pursuit-only integration. It does not alter the saved successful robot baseline.

On Ubuntu, update the existing clone and unpack the patch:

```bash
cd ~/nav2_follow_integration_repo
git pull --ff-only
base64 -d nav2-follow-goal-patch.tar.gz.b64 > nav2-follow-goal-patch.tar.gz
sha256sum nav2-follow-goal-patch.tar.gz
tar -xzf nav2-follow-goal-patch.tar.gz -C ~/nav2_follow_goal_patch
```

Expected SHA-256: `5add1bc6338007866905bb7f9bae07ff465087d4965309e79b133742e8e68348`.

Back up the current runtime files on the follower, then copy the four updated runtime files:

```bash
ssh sunuk@10.253.245.192 '
d=~/nav2_follow_integration/baseline/follower_diagnostics
mkdir -p "$d/backup_pre_goal"
cp "$d/run_local_avoidance_trial.py" "$d/follower_pursuit_preview.py" \
   "$d/follower_stamped_preview.py" "$d/local_trial_preflight.py" \
   "$d/backup_pre_goal/"
'

scp \
  ~/nav2_follow_goal_patch/baseline/follower_diagnostics/run_local_avoidance_trial.py \
  ~/nav2_follow_goal_patch/baseline/follower_diagnostics/follower_pursuit_preview.py \
  ~/nav2_follow_goal_patch/baseline/follower_diagnostics/follower_stamped_preview.py \
  ~/nav2_follow_goal_patch/baseline/follower_diagnostics/local_trial_preflight.py \
  sunuk@10.253.245.192:~/nav2_follow_integration/baseline/follower_diagnostics/
```

With the gate-wrapped Nav2 and follower sensors, bridge, and driver already running, start this pursuit-only trial on the follower:

```bash
python3 -B ~/nav2_follow_integration/baseline/follower_diagnostics/run_local_avoidance_trial.py \
  --run \
  --ack-clear-both-power-cut-ready \
  --follow-only \
  --follow-check-seconds 20 \
  --pose-source filtered \
  --reference-plan ~/nav2_follow_integration/baseline/follower_diagnostics/logs/new_map_reference_20261107.json \
  --nav2-leader \
  --seconds 360
```

When the follower prints that it is waiting for the RViz 2D Goal, enter the goal in RViz. The follower remains disarmed until it receives a valid Nav2 plan and prints the `START + Enter` prompt. If the obstacle appears, a required input becomes stale, or Nav2 changes the route during the run, the trial stops; this mode does not execute local avoidance.

Offline verification completed: 39 focused tests passed; the gate protocol simulation passed its 20,000-state randomized fault sweep and 80-second timeline. This is not a hardware-integrated pass.
