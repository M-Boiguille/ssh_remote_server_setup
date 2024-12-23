# SSH Remote Server Setup

Project from: [https://roadmap.sh/projects/ssh-remote-server-setup](https://roadmap.sh/projects/ssh-remote-server-setup)

The **SSH Remote Server Setup** project demonstrates how to automate the deployment and configuration of a remote server using Bash scripting. It streamlines tasks like creating a DigitalOcean droplet, configuring security, and deploying a simple website.

## Features

- Automatically creates a DigitalOcean droplet and retrieves its IP address.
- Generates and manages SSH keys for secure server access.
- Configures essential server security with UFW and Fail2Ban.
- Deploys static website files to the server using SCP.
- Handles retries for key operations, ensuring robust execution.

## Usage

### Workflow Overview

- **Trigger**:
  - Executes when the Bash script is run with the required environment variables.
- **Steps**:
  1. **Droplet Creation**:
     - Creates a new droplet and retrieves its public IP address.
  2. **Server Configuration**:
     - Configures SSH, sets up a firewall, and installs a web server.
  3. **Website Deployment**:
     - Copies static files to the server’s web root directory.

### Example Workflow Execution

1. Clone the repository and navigate to the project directory:
   ```bash
   git clone <repository-link>
   cd ssh-remote-server-setup
   ```

2. Set the DigitalOcean API token as an environment variable or pass it as an argument:
   ```bash
   export DOTOKEN=<your-token>
   ```

3. Run the script:
   ```bash
   ./setup-server.sh
   ```

4. The script will:
   - Create a droplet.
   - Configure SSH, UFW, Nginx, and Fail2Ban.
   - Deploy a static website to `/var/www/website`.

### Accessing the Deployed Site

- After successful deployment, access the website at:
  ```
  http://<droplet-ip>
  ```

## Development Environment

- **Tools Used**:
  - Bash scripting for automation.
  - `doctl` for interacting with the DigitalOcean API.
  - Linux utilities such as `ssh-keygen`, `ufw`, and `scp`.
- **Environment**:
  - Tested on a local Linux system.
  - Requires a DigitalOcean account with an API token.

## Improvements

- Add support for additional deployment targets such as AWS or Google Cloud.
- Integrate dynamic DNS for managing IP changes.
- Include advanced application deployment using Docker or Kubernetes.
- Enhance logging and error handling for better debugging.
- Implement notifications for script completion (e.g., Slack or email alerts).

## Example Workflow Configuration

Here’s an example of the workflow executed by the script:

```bash
#!/bin/bash

# Generate SSH keys
ssh-keygen -q -f keys_folder/roadmapkey1 -N ''

# Create droplet
doctl compute droplet create ssh-remote-server     --image ubuntu-24-04-x64     --size s-1vcpu-512mb-10gb     --ssh-keys <key-id>     --region ams3

# Configure server
ssh root@<droplet-ip> <<EOF
apt update
apt install -y nginx ufw fail2ban
EOF

# Deploy static website
scp index.html root@<droplet-ip>:/var/www/html/index.html
```

## Conclusion

The **SSH Remote Server Setup** project simplifies the deployment and configuration of remote servers with a streamlined Bash script. It is a practical solution for automating server provisioning and initial setup.

The [project link](https://roadmap.sh/projects/ssh-remote-server-setup).

Thanks to [https://roadmap.sh](https://roadmap.sh/).
