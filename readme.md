## Steps performed during Technical Assessment Nov 25, 3pm to 12mn

1. Inspect, install WSL Ubuntu 22 LTS
2. Create default WSL user/pass
3. Install, configure Docker Desktop, signup for docker hub
4. Test WSL integration
5. Install, configure VSCode 
   * setup WSL connection, docker integration

6. Test and refine mysql, phpmyadmin container configuration
   * Troubleshoot connection issue: wrong port between containers and host; disabled arbitrary
   * Install Windows client, test workbench
7. Sign up for github account, create repo, 2FA, generate personal access token classic with repo scope
8. Install windows and wsl git, not sure if this was integrated properly
9. Test windows Github Credentials Manager, switched to personal access token instead
10. Created local repo, connect to origin, start pushing code, work on dev branch
11. Configured nginx containers web1 and web2
12. Install ansible in Windows or WSL
13. Test, troubleshoot ansible tasks
    1. WSL docker integration needed full path to binary in windows filesystem
    2. used local connection for local docker deployment; disable gather facts
    3. setup and test deployment tasks for DB+UI
       1. down, rm containers
       2. collect files in dest path
       3. delete collected files
       4. clone repo
       5. up/build containers
14. Test, troubleshoot ansible vault setup and usage of encrypted variables
    1. vaulted vars are not working; just used plain text for sudo and git personal access token for now
15. Get a list of Nginx security best practices configuration. Was not able to start testing.

### These tasks were not performed due to lack of time
1. Apply security settings in nginx
2. Develop basic RESTful API with CRUD via http methods, for user registration 
3. Develop frontend web app with plain JS, connecting to API for user registration, login action, session mgt, input validation, CSRF.

### To clone the repo
**use the URL**
>https://github.com/ian8dev/devops-fullstack.git

**if username needed is:** `ian8dev`
**and personal access token**
> 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


### Deployment Notes:
1. The playbook file has been tested specifically on a WSL Ubuntu 22 installation.
2. Secrets are stored in plain text in the playbook for now. Further testing of encrypted variable usage is pending.
3. If deployment to a new instance of WSL is intended, the ff are needed:
   1. working docker desktop, docker-compose, git
   2. path of docker-compose binary should be explicitly configured if using the windows installed executable. 
4. When deploying to a common linux vm, at the least ansible should be installed, and installation of docker-compose and git can be handled in the playbooks.

### Deployment Steps:
1. Clone the repo
```bash

# git clone https://<personal-access-token>@github.com/ian8dev/devops-fullstack.git
# cd devops-fullstack/devops
```
2. Edit the `files web.yml`, `database.yml` line 11, provide your sudo password
```
ansible_become_pass: ""
```
3. Create deployment paths. This should have been included in the playbook.
```bash

# sudo mkdir -p /opt/deploy1 /opt/deploy2
```
4. Run playbooks
```bash

   # ansible-playbook database.yml
   # ansible-playbook web.yml
```
