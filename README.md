# alpine-drone-runner

Rôle ansible permettant de déployer des runners docker DRONE CI sur des machines
alpine linux.

**IMPORTANT: python3 doit être installé sur les machines cibles**

## Mode d'emploi

Tout d'abord, modifiez `ansible/hosts.ini` pour que cela corresponde à votre
config.

```
[runners]
drone-runner-hostname drone_runner_name=my-drone-runner
```

Ensuite, créez votre playbook :

```bash
cp ansible/{example-,}playbook.yml
```

Modifiez le fichier `ansible/playbook.yml`

```yaml
- name: install drone_runner
  hosts:
    - runners
  roles:
    - role: drone-runner
      drone_rpc_proto: https
      drone_rpc_host: drone.example.com # l'adresse de votre serveur drone
      drone_rpc_secret: my_rpc_secret # votre secret RPC drone
      drone_runner_capacity: 2
      # drone_runner_name is provided by the inventory
```

Et enfin, éxécutez le playbook

```
[user@host ansible]$ ansible-playbook ./playbook.yml
```

Et voilà!
