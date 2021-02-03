# References
* https://docs.ansible.com/ansible-tower/3.8.1/html/administration/openshift_configuration.html
* https://releases.ansible.com/ansible-tower/setup_openshift/ansible-tower-openshift-setup-3.8.1-1.tar.gz

# Environment options 
(see `.env`)
* REPO - The repository to publish images to, default is `jardilio` (will need to change, obviously)
* VERSION - The version to tag the created image as, default is `latest`
* PLAYBOOK - The playbook to execute, default is `install.yml`
* INVENTORY_FILE - The inventory to load, default is `./inventory/local-docker-desktop`)
* OPTIONS - Additional options to send to ansible-playbook command

# Instructions for local testing
* You need to have Docker installed with Kubernetes enabled in Docker Desktop first
* Run `docker-compose build` to build all images and log into redhat repo, if not already
* Then run `docker-compose run --rm ansible-tower-installer` to test deployment to local cluster

# Instructions for customized deploys
* Create a new inventory file in `./inventory` for the target
* Set `INVENTORY_FILE` to the path to this file (ie `./inventory/local-docker-desktop`)
* Then run `docker-compose run --rm ansible-tower-installer` to test deployment to new target

# Instructions for SDLC
* Set `VERSION` to tag release
* Build image artifact locally - `docker-compose build`
* Test deployment with local image - `docker-compose run --rm ansible-tower-installer`
* Push image to repository to leverage for future deployments - `docker-compose push`