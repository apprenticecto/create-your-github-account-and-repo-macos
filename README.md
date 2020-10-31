This simple repo illustrates the basic steps to create your [Github](github.com) account and your first repo.

### Create Your Github Account
- Set your unsername and password
- Enable MFA by selecting [your account security menu] (https://github.com/settings/security) - optional but recommended
- By using MFA, I recommend to use SSH to sync your local repos remotely on Gihub, as I had issues with HTTPS

### Get SSH Access
- [Generate your SSH key](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent); if you alrady have SSH keys in default folder, change name to the key or change location

### Add your SSH key to the ssh-agent
- enter `$ eval "$(ssh-agent -s)"`to start the ssh-agent in the background
- if the file `~/.ssh/config` does not exist, create it empty by entering `$ touch ~/.ssh/config`
- add to the file the following or modify its contents according to your ssh folder location and key name: 
  `$ Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa`
-Add your SSH private key to the ssh-agent and store your passphrase in the keychain: `$ ssh-add -K ~/.ssh/id_rsa`, using the correct path and name.

### Add your SSH Key to your Github Account
- [Add the new SSH key to your Github Account](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)
- On your Mac, open **"Keychain access"** and check if you already have entries for "github" (use search): delete them in case
- [Test your connection](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/testing-your-ssh-connection)

### Create Your First Repo
- Create a new repository on Github; you can decide if making it public (default) or private
- Enter `$ git clone <your repo ssh name>`
- Enter `$ cd <your repo name>`
- Enter `$ git config user.name "your username"`
- Type `$ git config --global user.email "your email address"`; be sure to use your [primary or added email address](https://github.com/settings/emails)
- Start coding locally, commit locally often and when you want to sync your remote repo enter `$ git push origin master`.
