# Linking Your PE Accounts to Your GitHub Accounts

## Prerequisites

1. You should already have your SoC Unix account, cluster access, and be able to `ssh` into one of the PE hosts.  If you are not able to do this, please look at the guide on the [programming environments](environments.md)
2. You should be comfortable with running basic UNIX commands.  If you have not gone through the UNIX guide and get your hands dirty, please [look at the guide and play with the various basic Unix commands](unix-essentials.md).
3. You should already have a GitHub account and can log into [GitHub.com](https://www.github.com).

## Purpose

Your will be using `git` (indirectly) for retrieving skeleton code and submitting completed assignments.  We will set up your accounts on PE hosts below so that `git` will be associated with your GitHub account.  This is a one-time setup.  You don't have to do this for every assignment.

## 1. Setting up `.gitconfig`

Create and edit a file called `.gitconfig` in **your home directory on the PE host**, with the following content:

```text
[user]
  name = Your Name
  email = Your Email
[github]  
  user = Your GitHub ID
```

Your email should be whatever you used to sign up GitHub (which may not be your SoC or NUS email).

For example, a sample `.gitconfig` looks like this:

```text
[user]
  name = Elsa
  email = queen@arendelle.gov
[github]  
  user = elsasnow16
```

After saving this file, run:

```
git config --get github.user
```

It should return your GitHub user id.

It should print your GitHub user id as already set.  If there is a typo, you need to edit `.gitconfig` again and reload it by repeating the command above.

## 2. Setting up Password-less Login

### Basic of SSH Keys

SSH uses _public-key cryptography_ for authentication.  The keys come in pairs: a public key and a private key.  The private key must be kept safe and known only to you.  You should keep the private key in your account, and not share it with others.

To authenticate yourself to another host or service, you configure the host/service with your public key.  When it is time for you to log in, your private key is "matched" with your public key.  Since only you know your private key, the service or the host can be sure that you are you and not someone else.

Suppose you want to log in from host X to host Y without a password.  You generate a pair of keys on X, then keep the private keys on X and store the public keys on Y.  If you want to [setup SSH Keys](environments.md#setting-up-ssh-keys) so that you can log into PE hosts from your computer without a password, for example, you generate the pair of keys on your computer (X) and then copy the public key to PE hosts.

Our goal now is to authenticate ourselves to GitHub from the PE hosts.  So, X is a PE host, and Y is GitHub.

### Generating SSH keys

The steps are explained in detail on [GitHub Docs](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).  Here is a summary of the steps that you should follow for CS2030S:

On any of the PE hosts, run
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```
where `your_email@example.com` is the email your associate with you used to sign up your GitHub account (i.e., the same one you entered in `.gitconfig`).

The command will prompt you where to save the key.  Just press ++enter++ to save into the default location, which is `$HOME/.ssh/id_ed25519`.

You will then be prompted for a passphrase.  Since our goal is to automate assignment submission without needing to type anything, you should enter an empty passphrase.  This increases the security risk, but then, we are working with CS2030S assignments here, not a top-secret project.  So empty passphrase will do.

You should see something like this:
```
ooiwt@pe119:~$ ssh-keygen -t ed25519 -C "ooiwt@comp.nus.edu.sg"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/o/ooiwt/.ssh/id_ed25519):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/o/ooiwt/.ssh/id_ed25519.
Your public key has been saved in /home/o/ooiwt/.ssh/id_ed25519.pub.
The key fingerprint is:
SHA256:Br3wg7mplVuPyuDz8yZVDSh8Mn5ls5+yPZhTvGzmAkk ooiwt@comp.nus.edu.sg
The key's randomart image is:
+--[ED25519 256]--+
|   .   .         |
|    = o.=        |
|   . =oo.=.      |
|   .E=.=o...     |
|  ..Bo=ooS. .    |
| . =o+.++ o      |
|  + +o = +       |
|   oo = O        |
|    .=oB..       |
+----[SHA256]-----+
```

### Adding Your CS2030S Public Key to Your GitHub Account


The next step involves logging into GitHub.com, click on your avatar on the top right corner, and choose "Settings".  Then choose "SSH and GPG keys" on the sidebar.

Then, click either "New SSH key" or "Add SSH key".  Enter an appropriate title for the key (e.g., "CS2030 PE Hosts").

Next, you need to paste your public key into the text box.  Go back to your terminal and run 

```
cat ~/.ssh/id_ed25519.pub
```

Remember that `cat` just dumps the content of the file to the standard output.  Now, you need to copy the content of the file displayed on the terminal, which is your public key, and paste it into the text box in the browser.  Your key should start with `ssh-ed22519` and ends with your email address.  For instance, this is the exact text that I copy-pasted:
```
ssh-ed25519 AAAZC3NzaC1lZDI1NTE8AAAAIDdmwMpRrhRB95u7CTahehtBEeOdhSxDQdlpCxBK3KCP ooiwt@comp.nus.edu.sg
```

I showed the above as an example, don't use my public key for your GitHub.  Otherwise, I will have access to your account :)

After entering the title and key above, click the green "Add SSH key" button to add the key you entered.  If prompted, confirm your GitHub password.

These steps are explained in detail on [GitHub Docs](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).

## 3. Checking Your Authentication Settings

To check if you can connect to `git@github.com` using SSH keys, run:
```
ssh -T git@github.com
```

If everything is set up correctly, you will see the message
```
Hi ooiwt! You've successfully authenticated, but GitHub does not provide shell access.
```

Otherwise, you should see
```
git@github.com: Permission denied (publickey).
```

or other error messages.

Note that you need to connect with the username `git`.  Do not use your GitHub username (e.g., do not use `ssh -T ooiwt@github.com`)

