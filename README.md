# SSH Setup between Localhost and Github
## Generating SSH Keys

1. Open a command line terminal and input the command > `ssh-keygen -t rsa -b 4096 -C "john.smith@email.com"` *(Use the same email address that is associated with your Gthub account)*
2. Input a logical key name, or leave it blank. Leaving this blank will generate a key with the default name `id_rsa`
3. **DO NOT GIVE THE KEY A PASSPHRASE**
4. Can use `ls` to see what has been generated. Should see 2 new items, `<keyname>` and `<keyname>.pub`

## Deploying .pub key to Github
1. Go to your Github settings
2. Go to `SSH and GPG keys`
3. Click `New SSH Key`
4. Give the key a logical title name
5. Navigate to your generated key pair from above and `cat` the `.pub` key. Copy **all** the text and paste it into the `key` section


# Creating CI
The end goal for this task is to push some sort of change to our Github repo, and have Jenkins automatically test the new code.
If the pushed code passes the tests, we want Jenkins to automatically merge our changes into the 'main' branch.

## Creating a Jenkins job
1. Go to your Jenkins page and select `New Item` at the top of the main menu list

    ![](./img/Jenkins_main_menu.PNG)

2. Enter a logical name for the job and select `Freestyle project`. Click `OK`.

---
1. Select the `Discard old builds` check-box and change the `Max # of builds to keep` to 3
2. Select the `GitHub project` check-box and input the relevant GitHub HTTPS link

![](./img/GitHub_http_url.PNG)

3. Select the `Restrict where this project can be run` check-box and in `	Label Expression`, input `sparta-ubuntu-node`.
4. Under `Source Code Management`, select the `Git` radio-button.
Under `Repositories`, input the SSH url in `Repository URL`
