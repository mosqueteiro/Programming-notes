# SSH Key notes  

---

## SSH Key setup

### Key generation  

from [github gist](https://gist.github.com/grenade/6318301):

```bash
ssh-keygen -t rsa -b 4096 -N '' -C "rthijssen@gmail.com" -f ~/.ssh/id_rsa
ssh-keygen -t rsa -b 4096 -N '' -C "rthijssen@gmail.com" -f ~/.ssh/github_rsa
ssh-keygen -t rsa -b 4096 -N '' -C "rthijssen@gmail.com" -f ~/.ssh/mozilla_rsa
```

### Key add

```bash
eval "$(ssh-agent -s)" # or eval `ssh-agent`
ssh-add ~/.ssh/id_rsa
ssh-add ~/.ssh/github_rsa
ssh-add ~/.ssh/mozilla_rsa
```

### File permissions  

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
chmod 644 ~/.ssh/known_hosts
chmod 644 ~/.ssh/config
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
chmod 600 ~/.ssh/github_rsa
chmod 644 ~/.ssh/github_rsa.pub
chmod 600 ~/.ssh/mozilla_rsa
chmod 644 ~/.ssh/mozilla_rsa.pub
```

or (shortened)

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/*
chmod 644 -f ~/.ssh/*.pub ~/.ssh/authorized_keys ~/.ssh/known_hosts
```

## Setting up `git` access  

* [Bitbucket ssh setup](https://confluence.atlassian.com/bitbucket/set-up-an-ssh-key-728138079.html)
