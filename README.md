# ansible.digitalocean.ubuntu
this repository houses a set of playbooks for automating the setup of servers over a set of standard Digital Ocean (DO) droplets running Ubuntu 22.04, and installing software for the development and execution of software. running it on other versions and systems may produce unexpected results.
  
there are three parts to this repository:  
`/inventories`: houses the dynamic inventory file for pulling basic information on DO resources in your account,  
`/playbooks`: houses app- and service-specific playbooks. these are all standalone and can be run accordingly, and  
`/main`: houses import files that allow you to run multiple playbooks at once. `server-docker.yaml` will run the initial server setup for a DO droplet running Ubuntu 22.04, install Docker and docker-compose, install the GitHub CLI client, and reboot the droplet.  
  
this is set as a template repository. use it to scaffold your own set of plays in addition to what's provided.  
  
## getting started
if you haven't already, install ansible:
```
sudo apt update
sudo apt install ansible
```
to ensure that all links work as intended, clone the repo to the root of your user account (`/home/your-username`). then
```
cd ansible-automation
```
copy `.env.temp` and rename it to `.env`:
```
cp .env.temp .env
```
open it and fill it out:  
`CREATED_USERNAME` is the non-sudo user you want to create when scaffolding a new server.  
`ALTERED_USER` is updating permissions for docker.  
`DO_API_KEY` is your DO API key.  
  
then export the contents to your shell's environment:
```
export $(cat .env | xargs) && env
```
you can, alternatively, manually enter these variables into your environment:
```
export KEY="value"
```
once you've got this completed, test the dynamic inventory file:
```
ansible-inventory -i ~/ansible-automation/inventories/digital_ocean.yaml --list
```
a list of available DO resources in your account will be listed. you can edit the `inventories/digital_ocean.yaml` file to adjust the attributes being requested, set up groups, and alter the filter.  
   
if everything works so far, run the playbooks as desired!  
