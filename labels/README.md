This script is used to add one or multiple labels to a specific node in a Docker Swarm cluster.

It connects remotely to the Swarm manager using SSH and applies labels to help with service placement, scheduling, and node organization.

📌 Purpose

Connects to a remote Docker Swarm manager

Assigns custom labels to worker/manager nodes

Verifies that labels were applied successfully

Displays the node’s current labels

Node labels are useful for:

Controlling where services run

Creating role-based nodes (db, proxy, storage, etc.)

Improving cluster management

⚙️ Configuration

By default, the script targets:

`ssh://ubuntu@10.0.1.115`

You can override this with either:

- `DOCKER_HOST` environment variable
- `--docker-host` option

Replace:

ubuntu → with your SSH user

10.0.1.115 → with your Swarm manager IP

Make sure SSH access is properly configured.

▶️ Usage
`./add-labels [--docker-host ssh://user@manager-ip] [--dry-run] <node_id> <label1=value1> [<label2=value2> ...]`

Example:
`./add-labels node-123 role=database zone=oran env=prod`

Dry-run example:
`./add-labels --dry-run --docker-host ssh://ubuntu@10.0.1.50 node-123 role=database`

🔍 What’s Improved

- Validates labels are in `key=value` format
- Supports `--dry-run` for safe previews
- Supports `--docker-host` for per-command target selection
- Uses safer shell settings (`set -euo pipefail`)
- Automatically cleans up exported `DOCKER_HOST`

⚠️ Important Notes

This script must be executed from a machine that has:

Docker installed

SSH access to the Swarm manager

Run the script with executable permissions:

`chmod +x add-labels`
