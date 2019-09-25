---
layout: post
title:  Signed Git commits
subtitle: Signing Git commits with GPG in SourceTree
published: true
categories: technology, git
---

You can sign your git commits with GPG to cryptographically verify the commit is really from you. I'm not going to cover how to sign a commit with a GPG key, but rather how to make this work with [SourceTree](https://www.sourcetreeapp.com/) (a good, free graphical Git tool). It isn't quite so straightforward as I found out.

SourceTree doesn't support code signing out of the box. We need to configure this in the git-bash shell that SourceTree uses behind the scenes. The below steps will detail the process to set this up.

## Setup GPG key

Generating a GPG key is quite straightforward, I won't repeat material that's found aplenty. Refer to [GitHub's link](https://help.github.com/articles/generating-a-new-gpg-key/) on how to. 

Once done, [add the key to Github](https://help.github.com/articles/adding-a-new-gpg-key-to-your-github-account/). We assume here the keys are generated on Ubuntu bash for Windows. Using any other tool like GPG4Win should work just as well.

## Identify the Keys

Here's the meat of this post. First, on the Ubuntu bash for Windows export your GPG keys (both public and private). Find the Key ID first. 

`gpg --list-keys`

The highted area is your key ID. You'll be using this in sections below `keyID`
![image](https://user-images.githubusercontent.com/32394146/40902455-a3426ad4-6806-11e8-86d7-03150d941d3c.png)


## Export the keys

Export the public key. Replace the text `<keyID>` with the ID as obtained above
`gpg --export <keyID> > public.key`

Export the private key
`gpg --export-secret-key -a <keyID> > private.key`

Copy the keys to a location on Windows say, `C:\`

## Add exported keys to SourceTree

Open SourceTree and within a repo, open the terminal:

![image](https://user-images.githubusercontent.com/32394146/40901678-d81873c8-6803-11e8-979c-caa14dece9d5.png)

This opens git-bash terminal. We need to import the GPG keys here. Navite to the folder where the keys were copied. In git-bash termial, the `C:\` drive is mapped as `/c` so navigate to that folder: `cd /c/`

See if there are any keys already present here
`gpg --list-keys`

Now import the two keys:

`gpg --import public.key`

`gpg --allow-secret-key-import --import private.key`

## Configure SourceTree to Sign all requests

Set git to sign all commits with the following command:

`git config commit.gpgsign true`

Since the git-bash shell was opened within a particular repo, this will add to the config file of that repo only. To instruct git to sign ALL commits globally, add the `--global` flag to the above command: 

`git config --global commit.gpgsign true`

This will edit the `C:\Users\<user>\.gitconfig` global file for the Git installation on that machine. Open this config file and you can see the below section added: 

```
[commit]
	gpgsign = true
```

{: .box-note}
**Note:** An easier way would be to just edit the `.git\config` by hand and add the above section.



## Specify GPG Key to use
	
We now need to specify WHAT key to use to sign (there may be many keys in the GPG keyring). This is done by the git command:

`git config user.signingkey <keyID>`

As above, you can issue this command local to a repo or globally by adding the `--global` flag.

The corresponding config file will be edited to add the key (say, &lt;keyID&gt; = 25FA525E)

```
[user]
	signingkey = 25FA525E
```

{: .box-note}
**Note:** You can add the `signingkey` on a per repo basis or globally



## Test! 

Now commit and push using git-bash or SourceTree. You can see that your commits are now "Verified"

![image](https://user-images.githubusercontent.com/32394146/40902918-319d113e-6808-11e8-851e-21f809592409.png)


{: .box-note}
**Reference: [GitHub: Signing Commits](https://help.github.com/articles/signing-commits-using-gpg/)**