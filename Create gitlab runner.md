
Create new file setup-runner.sh with this content

```
#!/bin/sh

set -e

AIASSET_NAME=$1
URL=$2
TOKEN=$3

echo "Downloading GitLab runner..."
echo $AIASSET_NAME
echo $URL
echo $TOKEN

# Deploy runner
docker run -d --name ${AIASSET_NAME} --restart always \
	-v /srv/gitlab-runner/config:/etc/gitlab-runner \
	-v /var/run/docker.sock:/var/run/docker.sock \
     	gitlab/gitlab-runner:latest


echo "Deploying GitLab runner..."
# Register runner
docker run --rm -v /srv/gitlab-runner/config:/etc/gitlab-runner gitlab/gitlab-runner register \
  --non-interactive \
  --executor "docker" \
  --docker-image docker:latest \
  --url ${URL} \
  --registration-token ${TOKEN} \
  --description ${AIASSET_NAME} \
  --tag-list "bonseyes" \
  --run-untagged="true" \
  --locked="true" \
  --access-level="not_protected"

# Edit conf
sudo sed -i '/output_limit = /d' /srv/gitlab-runner/config/config.toml
sudo sed -i 's|executor = "docker"|executor = "docker"\n  output_limit = 100000|g' /srv/gitlab-runner/config/config.toml
sudo sed -i 's|concurrent = 1|concurrent = 10|g' /srv/gitlab-runner/config/config.toml
sudo sed -i 's|volumes = \["/cache"\]|volumes = \["/cache", "/var/run/docker.sock:/var/run/docker.sock"\]|g' /srv/gitlab-runner/config/config.toml

# Restart to apply changes
docker restart $AIASSET_NAME
```

run this command

```
sudo bash ./setup-runner.sh {runner_name} {url like this https://gitlab.com/} {replace with gitlab runner token}

```
 sample 
 ```
 sudo bash ./setup-runner.sh dashboard_api_cicd_r https://gitlab.com/ GR1348941k28zC6MQd-zy91dUzau1
 ```



