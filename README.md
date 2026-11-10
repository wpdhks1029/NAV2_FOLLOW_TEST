# Nav2 leader goal + follower Pure Pursuit

This is an isolated experiment branch. It leaves the saved successful backup and `final_robot` untouched.

## Refresh the deployment bundle on Ubuntu

```bash
cd ~/nav2_follow_integration_repo
git pull --ff-only
base64 -d nav2-follow-goal-deployment-v2.tar.gz.b64 > nav2-follow-goal-deployment-v2.tar.gz
sha256sum nav2-follow-goal-deployment-v2.tar.gz
tar -xzf nav2-follow-goal-deployment-v2.tar.gz -C ~/nav2_follow_integration
```

Expected SHA-256: `b8b1fe64896a6ff26a30cf9b5a54b5195a1a409c1924c3035a6aa53dc3c92934`.

Copy the two updated follower files to the follower computer (keep the earlier integration bundle and gate files in place):

```bash
scp ~/nav2_follow_integration/baseline/follower_diagnostics/run_local_avoidance_trial.py \
    ~/nav2_follow_integration/baseline/follower_diagnostics/local_trial_preflight.py \
    sunuk@10.253.245.192:~/nav2_follow_integration/baseline/follower_diagnostics/
```

## Run for RViz goal following

On the follower, start the existing standard hardware driver (non-continuous20), sensors, localization, and bridge. In the follower trial terminal run:

```bash
source /opt/ros/humble/setup.bash
source ~/robot_ws/install/setup.bash
export ROS_DOMAIN_ID=10
export ROS_LOCALHOST_ONLY=0

python3 -B ~/nav2_follow_integration/baseline/follower_diagnostics/run_local_avoidance_trial.py \
  --run \
  --ack-clear-both-power-cut-ready \
  --follow-only \
  --auto-start-on-goal \
  --follow-check-seconds 360 \
  --pose-source filtered \
  --nav2-leader \
  --seconds 360
```

Then click **2D Goal Pose** in the leader Nav2 RViz. The process arms on active `NavigateToPose`, checks the follower's fresh map pose, scan, motor status, and the exclusive gate graph, then follows the leader bridge's measured `/leader/path` with Pure Pursuit. It does not run follower local obstacle avoidance. A 0.04 m/s leader startup crawl lets that measured path form; after path tracking begins, missing/stale path or unsafe scan stops the system. Goal completion, cancellation, or failure disarms the follower and closes the leader gate.

For follower initial pose, the RViz `SetInitialPose` tool must publish `/follower/initialpose`; verify AMCL convergence on `/follower/amcl_pose`. The bundled `convoy_view.rviz` has that topic configured.

## Offline checks

40 unit tests passed. The gate protocol simulation passed 1,600 state transitions and a seeded 20,000-state fault sweep. This checks software logic only; it does not establish physical robot success.
