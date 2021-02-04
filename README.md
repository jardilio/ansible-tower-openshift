# References
* https://docs.ansible.com/ansible-tower/3.8.1/html/administration/openshift_configuration.html
* https://releases.ansible.com/ansible-tower/setup_openshift/ansible-tower-openshift-setup-3.8.1-1.tar.gz

# Environment options 
(see `.env`)
* REPO - The repository to publish images to, default is `jardilio` (will need to change, obviously)
* VERSION - The version to tag the created image as, default is `latest` (should be set to increment during CI process)
* PLAYBOOK - The playbook to execute, default is `install.yml`
* INVENTORY_FILE - The inventory to load, default is `./inventory/local-docker-desktop`
* OPTIONS - Additional options to send to ansible-playbook command

# Instructions for local testing
* You need to have Docker installed with Kubernetes enabled in Docker Desktop first
* Run `docker login registry.redhat.io` to pull images (create account first if not already)
* Run `docker-compose build` to build all images locally to run
* Then run `docker-compose run --rm ansible-tower-installer` to test deployment to local cluster

# Instructions for customized deploys
* Create a new inventory file in `./inventory` for the target
* Set `INVENTORY_FILE` to the path to this file (ie `./inventory/local-docker-desktop`)
* Then run `docker-compose run --rm ansible-tower-installer` to test deployment to new target

# Instructions for SDLC
* Set `VERSION` to tag release
* Log into the required reposorities - `docker login registry.redhat.io`
* Build image artifact locally - `docker-compose build`
* Test deployment with local image - `docker-compose run --rm ansible-tower-installer`
* Test removal of deployment - TODO
* Push image to repository to leverage for future deployments - `docker-compose push`
* Run deployment to all targets - TODO