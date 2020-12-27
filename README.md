This simple README illustrates the basic steps to create your [Github](github.com) account and your first repo, with GPG integrated features.

### Create Your Github Account
- Set your username and password
- Enable MFA by selecting [your account security menu] (https://github.com/settings/security) - optional but recommended
- By using MFA, I recommend using SSH to sync your local repos remotely on Github, as I had issues with HTTPS

### Get SSH Access
- [Generate your SSH key](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent); if you already have SSH keys in the default folder, change the name to the key or change location

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

### Sign Your Commits

#### Create your PGP Key

Install GPG with `brew install gnupg` or update it with `brew upgrade gnupg`.

Create your [PGP Key](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-gpg-key).

You need an RSA 4096 key. Add your username and email.

After creation, launch the command `gpg --list-secret-keys --keyid-format LONG`, to check your newly created key. 

#### Import you GPG Key from Keybase

The above command can be used also in case you already generated your key.

In case you've uploaded your GPG key on [keybase](keybase.io), you can import your public key a txt by launching the command `keybase pgp export | gpg --import`.

#### Export your PGP Public Key and Add it to GitHub

After, you need to export your public key, by launching the command `gpg --armor --export youremail@email.com` matching your email address with the one used to create the GPG key.

If you can't remember what email address is attached to your public key, you can list all your gpg keys with `gpg --list-keys`. See this [well-explained article](https://www.elliotblackburn.com/importing-pgp-keys-from-keybase-into-gpg/). 

Now you can copy and paste the output and copy into GitHub, by selecting the "settings" option within your profile and add the GPG Key.

#### Use The Key to Sign Your Commits

On your local repo, you need to add the following information:

- username, by launching the command `git config --global user.name "your_username"`
- signkey, by launching the command `git config --global user.signingkey your_ Key_ID`
- email, by launching the command `git config --global user.email "your_email_address"`, matching the address used for your GPG key.

Once you commit, locally, use `git commit -S -m your commit message`, unless auto-sign command has been entered (see below).

### Create Your First Repo
- Create a new repository on Github; you can decide if making it public (default) or private
- Enter `$ git clone <your repo ssh name>`
- Enter `$ cd <your repo name>`
- Enter `$ git config user.name "your username"`
- Enter `git config --global user.signingkey your_ Key_ID`, to add your signkey
- Type `$ git config --global user.email "your email address"`; be sure to use your [primary or added email address](https://github.com/settings/emails), which needs to match the email used to generate your GPG key, too
- Add `git config --global commit.gpgsign true` to auto-sign iwht your key each commit
- Start coding locally, commit locally often and when you want to sync your remote repo enter `$ git push origin master`
- Check on your commits on Github: you should see "verified".

### Troublehooting
In case you should get this message after a commit:
```
error: gpg failed to sign the data
fatal: failed to write commit object
```

Enter `echo 'no-tty' >> ~/.gnupg/gpg.conf` and then `export GPG_TTY=$(tty)` to apply change to all users.

See [this stackoverflow thread](https://stackoverflow.com/questions/39494631/gpg-failed-to-sign-the-data-fatal-failed-to-write-commit-object-git-2-10-0) for more information and cases.

## Documentation

- [Github - Managing commit signature verification](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/managing-commit-signature-verification)
