# Project to deploy a K8s cluster

The main goal of this project is to deploy a k8s cluster in AWS by only using Ansible.

## Project steps

```
- Provisionning => we'll provision all the necessary infrastructure in AWS for our cluster.
- Cluster install => we'll install the k8s cluster.
- Deploy => using Helm to deploy our applications.
```

## Usage

First step is to create your API Token for Ansible to interate with Digital Ocean API properly. To do so, Login to your DO Account, go to API in the left panel, click in the Generate New Token. Copy/Save this token, because you'll not be able to see it once again in this page.  

Now, open your `Terminal` and type the following command:  

```bash
$ ansible-vault encrypt_string --stdin-name 'digitalocean_token'
```
Where:  
    `digitalocean_token` - is the variable name that you're going to store/pass your token.

Ansible Vault will ask you for a `Password`, type it 1st time and hit `Enter`, then type it once again to confirm and hit `Enter` once again. After that, you can paste your `Token` to be encrypted *DO NOT HIT ENTER*, otherwise, it will add a newline character in the end of the file, instead, hit ctrl-d (perhpas you have to hit it twice).  

Ansible will print out your encrypted string. Pay special attention because you haven't hitted `Enter`, therefore Ansible has printed out your encrypted string together with the end of the pasted `Token`.  

Ex:  
```bash
digitalocean_token: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          61643831303735646231326564633734393064653463386365303637343031663834386366353865
          3362303134336535306566306561356239373132363433370a393965323233323763663062373435
          32336630393938613334633169353764633364353133326161393166323135353661333961343930
          6638383136396330300a353166663264346436613733386362363605663762613064653530656262
          66333764663532626536353232363962623662633737656539653961333565383761643165326263
          32373836353336613630643931333639616464663361393265356265383934393035323135386165
          30356531393234616439306465643438313532326536366461356466346535623536343337636138
          39353930336463643464
```

Paste that string to your vars/main.yml file.

Now, when you'd run your `playbook`, you have to add `--ask-vault-pass` and Ansible will ask your password to decrypt your variable. If you don't want to type the password, just provide a text file containing the password and provide `--vault-password-file /path/to/my/vault-password-file` as argument instead of `--ask-vault-pass`.

## License
