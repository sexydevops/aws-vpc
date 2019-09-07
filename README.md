# AWS VPC

## EC2
### Connect to a private subnet instance

- In your local computer make sure you have SSH client
- Create Bastion host inside VPC that have public IP (use Elastic IP is better)
- Copy key to Bastion host:

```
ssh-copy-id username@ip
```
or :
```
ssh-copy-id -i identity_file username@ip
```
if `identity_file` is not provided, it will specific the file `~/.ssh/id_rsa.pub`
- Setup SSH config file: `vim ~/.ssh/config`

```
Host bastionhost
   HostName ipofbastionhost
   User yourusername
Host privatehost
   HostName privateip
   User ec2-user
   IdentityFile yourfile.pem
   ProxyCommand ssh bastionhost -W %h:%p
```

- Then `ssh privatehost` should work.
