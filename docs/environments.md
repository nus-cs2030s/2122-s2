# The CS2030S Programming Environment

## Java version

Java is a language that continues to evolve.  A new version is released every six months.  For CS2030S, we will _only_ use Java 11, the second most recent version with long-term support[^1].  Specifically, we use `openlogic-openjdk-11.0.8+10` on Ubuntu 20.04.3 LTS.

## Programming Servers

The school has provided a list of computing servers for you to use, with all the required software for CS2030S installed.  You can access them remotely via `ssh`, or secure shell.  The hosts are named `pe111`, `pe112`, ... , `pe120`.  (`pe` stands for "programming environment").  We will refer to these servers generally as the _PE hosts._

For this semester, the two servers `pe115` and `pe116` are not available.

You can choose which of the eight hosts to use.  You share the same home directory across all the hosts (this home directory, however, is different from that of `stu1`).  If you notice that one host is crowded, you can use another host to spread out the load.

While you can complete the programming assignments on your computers, the practical exams are done in a controlled environment using servers similar to the PE hosts.  It is therefore advisable for you to familiarize yourself with accessing the PE servers via `ssh` and edit your program with either `vim` or `emacs` (`vim` is recommended and supported).

## Accessing CS2030S Programming Environment

### Basic Requirements

1. You should be familiar with the terms Unix, command-line interface, command prompt, terminal, and shell.  Read this [background article](unix-background.md) if you don't.

1. You need to have an SoC Unix account.  If you do not have one, you can [apply for one online](https://mysoc.nus.edu.sg/~newacct/).

2. Once you have an account, you need to [activate your access to the PE hosts](https://mysoc.nus.edu.sg/~myacct/services.cgi), which is part of the SoC computer clusters.

3. You need a command-line `ssh` client.  Windows 10, macOS, and Linux users should already have it installed by default.

    For older versions of Windows, such as those used in the SoC's programming labs, you can check out [XShell 6](https://www.netsarang.com/en/free-for-home-school/) (free for home/school use), or [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).  These are GUI-based programs so the command line instructions below do not apply.

4. You need a good [terminal](unix-background.md#what-is-a-terminal) app.  There are many choices, but we recommend [Windows Terminal](https://docs.microsoft.com/en-us/windows/terminal/) for Microsoft Windows users; the default [Terminal](https://support.apple.com/en-sg/guide/terminal/welcome/mac) or [iTerm2](https://iterm2.com/index.html) for macOS users.  

### Testing Your SoC Unix Account

You can skip this step if you have been using your SoC Unix account and is familiar with your SoC Unix username and password.

1. Launch the terminal app on your computer.

2. At the command prompt, connect to SoC Unix server `stu.comp.nus.edu.sg` with the secure shell `ssh`.  The basic command to `ssh` is

```
ssh <username>@<hostname>
```

Replace `<hostname>` with the host you want to log into and `<username>` with your SoC Unix username.  Note that both are case-sensitive.

For instance, I would do:
```
ssh ooiwt@stu.comp.nus.edu.sg
```
to log into `stu.comp.nus.edu.sg`.

After the command above, follow the instructions on the screen.  The first time you ever connect to a host, you will be warned that you are connecting to a previously unknown host.  

```
The authenticity of host 'stu.comp.nus.edu.sg (137.132.80.61)' can't be established.
ED25519 key fingerprint is SHA256:sLdNXdswjUgsZjYJ5O+us3nAQIfgO2xWIT1C7JhrI+4.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Say `yes`, and you will be prompted with your password for that host.  Type in your SoC Unix password.  Note that passwords are case-sensitive, and nothing will be shown on the screen as you type your password for security reasons.  Press ++enter++ when you are done.  You should see something like this:

```
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-91-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Tue 04 Jan 2022 10:42:35 AM +08

  System load:  0.0               Processes:               217
  Usage of /:   7.8% of 49.98GB   Users logged in:         2
  Memory usage: 10%               IPv4 address for enp0s4: 192.168.49.55
  Swap usage:   0%

 * Super-optimized for small spaces - read how we shrank the memory
   footprint of MicroK8s to make it the smallest full K8s around.

   https://ubuntu.com/blog/microk8s-memory-optimisation

0 updates can be applied immediately.


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

Last login: Tue Jan  4 10:37:33 2022 from 137.132.80.61
ooiwt@stu1:~$
```

If you have reached this step, your SoC Unix username and password are working.

Type ++ctrl++ ++d++ to exit before continuing with the next step. 

### Accessing The PE Hosts

This is the step that you need throughout the semester to access the PE hosts.

The PE hosts can only be accessed from within the School of Computing networks.  This is not an issue during your lab sessions, but if you wish to access the PE hosts from outside of SoC, you need to tunnel through `stu.comp.nus.edu.sg`.

The server (`stu.comp.nus.edu.sg`) is configured to allow your connection if it's originating from a local telco (See [more details here](https://dochub.comp.nus.edu.sg/cf/guides/unix/soc_unix_pass_your_direct_access_to_soc_unix_servers)).

Since `stu.comp.nus.edu.sg` is within the SoC network, you can log into `stu.comp.nus.edu.sg` first, then from `stu.comp.nus.edu.sg`, log into one of the PE nodes.  These two steps can be done with one command:
```
ssh -t <username1>@stu.comp.nus.edu.sg ssh <username2>@<pe1xx>.comp.nus.edu.sg
```

- In non-exam scenarios, replace `username1` and `username2` with your SoC Unix username and `pe1xx` with one of `pe111` to `pe120`.  You will be prompted for your password twice.  The first prompt will be for your password to `stu.comp.nus.edu.sg`, and the second, to `pe1xx.comp.nus.edu.sg`.  Again, in a non-exam scenario, they will both be your SoC Unix password.
- For practical exams, you will be issued a special exam account to log into the PE hosts.  In this case, `username1` will be your SoC Unix username and `username2` will be your special exam account. 

You should see something like this:
```
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-91-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Tue 04 Jan 2022 10:50:56 AM +08

  System load:  0.0                Processes:             281
  Usage of /:   13.1% of 46.54GB   Users logged in:       0
  Memory usage: 2%                 IPv4 address for eno1: 192.168.48.122
  Swap usage:   0%                 IPv4 address for eno2: 192.168.57.122

 * Super-optimized for small spaces - read how we shrank the memory
   footprint of MicroK8s to make it the smallest full K8s around.

   https://ubuntu.com/blog/microk8s-memory-optimisation

0 updates can be applied immediately.


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

Last login: Wed Nov  3 07:51:42 2021 from 192.168.49.36
ooiwt@pe120:~$
```

This means you have successfully connected to the CS2030S programming environment.

You can now proceed to do three things:

- learn about the [basic Unix commands](unix-essentials.md) to navigate your home directory and manipulate files.
- learn about how to edit a file in `vim`, by running the command `vimtutor`.  A [CS2030S vim guide](vim-philosophy.md) is also available.
- [set up password-less login to the PE hosts](environments.md#setting-up-password-less-login)

### Troubleshooting

If you get the following error:

1. `ssh: Could not resolve hostname pe1xx.comp.nus.edu.sg`

    `ssh` cannot recognize the name `pe1xx`. Likely, you tried to connect to the PE hosts directly from outside of the SoC network.

2. `Connection closed by 192.168.48.xxx port 22`

    You have connected to the PE host, but you are kicked out because you have no permission to use the host.

    Make sure you have activated your access to "SoC computer clusters" [here](https://mysoc.nus.edu.sg/~myacct/services.cgi)

3. `Permission denied, please try again`

    You did not enter the correct password or username.  Please use the username and password
of your SoC Unix account which you have created here: https://mysoc.nus.edu.sg/~newacct/.  

    Check that you have entered your username correctly.  It is _case-sensitive_.

    If you have lost your password, go here: https://mysoc.nus.edu.sg/~myacct/iforgot.cgi

4. `ssh: connect to host stu.comp.nus.edu.sg port 22: Operation timed out`

    It means that you failed to connect to `stu.comp.nus.edu.sg` via `ssh`.  There could be two reasons for this: (i) `stu.comp.nus.edu.sg` or its ssh service is down; (ii) you are connecting via a network where `stu.comp.nus.edu.sg` is not accessible (such as outside Singapore).  

    The likelihood of (i) is small.  The more likely scenario is (ii).  In either case, connect to [SoC VPN](https://dochub.comp.nus.edu.sg/cf/guides/network/vpn?s[]=vpn) first, then `ssh` into one of the PE host.

5. `Could not chdir to home directory /home/o/ooiwt: Permission denied`

    This error means that you have successfully connected to the PE hosts, but you have no access to your home directory.

    This should not happen.  Please send an email with the above error message to `helpdesk@comp.nus.edu.sg`, include the PE hosts that you connected to with this error and your username.  The system administrator can reset the permission of your home directory for you.

### Setting up Password-less Login

To avoid typing in your password repeatedly, you can change the way you authenticate yourself to `stu.comp.nus.edu.sg` and the PE hosts, from using a password to using _public-key cryptography_ for authentication.  The keys come in pairs: a public key and a private key.  The private key must be kept safe and known only to you.  You should keep the private key in your account, and not share it with others.

To authenticate yourself to another host or service, you configure the host/service with your public key.  When it is time for you to log in, your private key is "matched"[^2] with your public key.  Since only you know your private key, the service or the host can be sure that you are you and not someone else.

The following is a one-time setup to enable this.

Let's say you want to log in from Host A to Host B.  On Host A, run:
```
ssh-keygen -t rsa
```

to generate a pair of keys on Host A.  When prompted, you can save the file `id_rsa` in the default location `~/.ssh` and enter an empty passphrase.  

{++Expanded++} What the command above does is it creates two files, the private key `id_rsa` and the public key `id_rsa.pub`.  Next, you need to plant the public key on Host B.  There are two ways to do this:

#### Method 1: Using `ssh-copy-id`

If Host A has `ssh-copy-id` installed, then, on Host A, run:
```
ssh-copy-id <username>@<hostname of B>
```

You will be prompted to enter your password for Host B.  After this step is completed, your public key will be copied to and configured for password-less login to Host B.  

#### Method 2: Manually copy the public key to Host B.

First, you need to copy the public key id_rsa.pub to your home directory on the remote host you want to log into.  We will use `scp`, or secure copy, for this.  On Host A,

```
scp ~/.ssh/id_rsa.pub <username>@<hostname of B>
```

You will be prompted with your password to login to transfer the file.

Then, log into the Host B, run,

```
cat id_rsa.pub >> ~/.ssh/authorized_keys
```

to add your public key to the list of keys.

Make sure that the permission for `.ssh` on Host A and Host B are set to 700 and the files `id_rsa` on Host A and `authorized_keys` on Host B are set to 600.  See the [`ls`](unix-essentials.md#ls-list-content-of-a-directory) and [`chmod`](unix-essentials.md#file-permission-management)

After using either one of the methods above, you should be able to `ssh` into Host B without using being prompted for a password every time.

Recall that to log in to a PE host, you need to two steps, first from your local computer to into `stu.comp.nus.edu.sg`, then from `stu.comp.nus.edu.sg` into `pe1xx.comp.nus.edu.sg`.  So to setup password-less login to `pe1xx.comp.nus.edu.sg`, you need two steps.  

For example, using Method 1 (`ssh-copy-id`), you need to do the following.

First, on your local computer:
```
ssh-keygen -t rsa
ssh-copy-id <username>@stu.comp.nus.edu.sg
```

Then, on `stu.comp.nus.edu.sg`:
```
ssh-keygen -t rsa
ssh-copy-id <username>@pe1xx.comp.nus.edu.sg
```

Since all the PE hosts share the same file directory, you only need to do this for one of the PE hosts.  After this one-time step, you can log in without a password to any one of the PE hosts.

## Stability of Network Connections

Note that a stable network connection is required to use the PE hosts for a long period without interruption. If you encounter frequent disconnections while working at home or on campus while connected wirelessly, please make sure that your WiFi signal is strong and there is no interference from other sources. 

If you find yourself facing frequent disconnection, you can consider running [`screen`](https://en.wikipedia.org/wiki/GNU_Screen).  After logging into a PE host, run:
```
screen
```

You will see some messages, press ++enter++ to go to the command prompt.  You can now use the PE host as usual.  In case you are disconnected (e.g., in the middle of editing), you can log into the same PE host again, and run:
```
screen -r
```

to resume your previous session.

[^1]: The latest Java LTS version is 17.

[^2]: I skipped many cool details here.  This topic is part of CS2105 and CS2107.  Interested students can google up various articles and videos online about how public-key cryptography is used for authentication.
