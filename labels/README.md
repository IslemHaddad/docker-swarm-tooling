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

Before using the script, update the Docker host address:

export DOCKER_HOST="ssh://ubuntu@10.0.1.115"


Replace:

ubuntu → with your SSH user

10.0.1.115 → with your Swarm manager IP

Make sure SSH access is properly configured.

▶️ Usage
./add-labels.sh <node_id> <label1=value1> [<label2=value2> ...]

Example:
./add-labels.sh node-123 role=database zone=oran env=prod


This will apply the following labels to the node:

role=database

zone=oran

env=prod

🔍 How It Works

Sets the DOCKER_HOST variable to connect to the remote Swarm manager.

Reads the first argument as the node ID.

Processes all remaining arguments as labels.

Applies each label using:

docker node update --label-add


Stops execution if any label fails.

Displays the final list of labels.

Unsets the DOCKER_HOST variable after execution.

⚠️ Important Notes

This script must be executed from a machine that has:

Docker installed

SSH access to the Swarm manager

Always verify and update DOCKER_HOST before running.

Run the script with executable permissions:

chmod +x add-labels.sh