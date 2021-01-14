## GITHUB ACTIONS - CONTINUOUS DEPLOYMENT

**_First we need to make sure that we can `git pull` our repo from the server without being prompted to enter git credentials. To do so we will need to:_**

### Generate new server SSH key and add it to the repo

- on your server navigate to `/home/<user>/.ssh`
- run `ssh-keygen -m PEM -t rsa -b 4096 -C "key_name"` to generate a new ssh key pair
- copy the contents of the **public** key `cat key_name.pub`
- open your GH repo settings, and navigate to deploy keys -> add deploy key
- create a meaningful title and paste the contents of your server **public** key
- if you're not going to push code from your server you might leave 'allow write access' unchecked

**_We might have multiple repos on the server, so it's a good idea to configure what keys should be used for each of them:_**

### SSH config

- on your server navigate to `/home/<user>/.ssh`
- create or open the config `nano config`
- sample config:

```
Host github.com
    Hostname github.com
    IdentityFile=/home/<user>/.ssh/<key_name>
    IdentitiesOnly yes
```

**_Then we need to make sure that our repo's remote uses SSH protocol:_**

### Make sure repo remote uses SSH not HTTPS

- on server navigate to your repo
- run `git remote -v` to see what protocol is used
- if the link starts with https
  - open your repo on GH and copy the ssh link to it
  - run `git remote set-url origin git@github.com:<org_name>/<repo_name>.git`

**_That's it, you can try to run `git pull` now to see if it works. <br> The next step will be allowing our GH repo to establish SSH connection with the server. To do so we will need to:_**

### Generate new private key and add it to the repo

- on your local machine generate new ssh key by running:
  `ssh-keygen -m PEM -t rsa -b 4096 -C "key_name"`
- navigate to `/home/<user>/.ssh`
- copy the contents of the **private** key `cat key_name`
- open your GH repo settings, and navigate to secrets -> new repository secret
- create the name (will be used in the configuration code <a href="#action">below</a>), and paste the contents of the **private** key

**_Then we will need to:_**

### Add public key to the server

- on local machine navigate to `/home/<user>/.ssh`
- on local machine copy the contents of the **public** key `cat key_name.pub`
- on server navigate to `/home/<user>/.ssh`
- on server run `nano authorized_keys` and paste the contents of your **public** key
- this might require server ssh service restart `sudo systemctl restart sshd`

**_Once everything is set up we can finally create out github action that will ssh to our server, pull all new changes and apply all the necessary steps to deploy our new build:_**

### Starting github workflows
[Credits for this step](https://www.youtube.com/watch?v=gW1TDirJ5E4&ab_channel=omgneering)

- in the root of your repo create a new dir .github/workflows
- create your_workflow_name.yml
- <a name="action"></a>sample configuration:

```
name: YourName #arbitrary project name
on: #what event will trigger the action
  push: #will also work on merging PRs
    branches: [ master ] #list of branches that will trigger the event

jobs: #list of jobs to start
  job_one: #arbitrary job name
    name: Deploy #arbitrary name
    runs-on: ubuntu-latest #what OS use to run the action
    steps:
    - name: deploying my_project #the name that will be displayed when the task runs
      uses: appleboy/ssh-action@master #marketplace extension to use ssh
      with:
        host: myserver.com #what server to connect to
        username: username #server credentials
        key: ${{ secrets.MY_SSH_KEY }} #private key reference (secret name from above)
        port: 22 #default ssh port
        script: | #what commands to run on your server to deploy the app, e.g. (note the pipe character)
          cd projects/my_project
          git pull origin master
          python3 manage.py migrate
          echo "yes" | python3 manage.py collectstatic
          cd ..
          sudo docker-compose up --build -d
```

[Go back](../README.md)
