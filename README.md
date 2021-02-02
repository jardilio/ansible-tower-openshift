Reference: https://docs.ansible.com/ansible-tower/3.8.1/html/administration/openshift_configuration.html
Source: https://releases.ansible.com/ansible-tower/setup_openshift/ansible-tower-openshift-setup-3.8.1-1.tar.gz

Need to have Docker installed with Kubernetes enabled in Docker Desktop. Run `init` first time to login and create creds. Then run `docker-compose run --rm deploy` to test deployment to local cluster. 

Note: Currently fails to authenticate to redhat repo to pull the required images for AWX.