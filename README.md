# cloudbox_mod
Blank Template to add custom Ansible roles.

## How to use this template

1. Clone this repo:

    ```bash
    git clone https://github.com/cloudbox/cloudbox_mod.git ~/cloudbox_mod
    ```

1. CD into the `cloudbox_mod` folder:

    ```bash
    cd ~/cloudbox_mod
    ```

1. Create folders for the Ansible role:

    ```bash
    mkdir -p ~/cloudbox_mod/roles/myrole/tasks/
    ```

1. Place the task file there:

    ```bash
    touch ~/cloudbox_mod/roles/myrole/tasks/main.yml
    ```

1. Add custom variables into settings:

    ```
    ~/cloudbox_mod/settings.yml
    ```

1. Add the Ansible role to `cloudbox_mod.yml`:

    ```bash
    nano ~/cloudbox_mod/cloudbox_mod.yml
    ```

    ```yaml
    ---
    - hosts: localhost
      vars_files:
        - settings.yml
        - /home/seed/cloudbox/settings.yml
      roles:
        - { role: myrole, tags: ['myrole'] }
    ```

1. Run the Ansible role:

    ```bash
    sudo ansible-playbook cloudbox_mod.yml --tags myrole
    ```


## How to mod a Cloudbox role

1. Copy the Ansible role you want to modify from `~/cloudbox/roles` to `~/cloudbox_mod/roles`.

   For example:
   ```
   cp -r ~/cloudbox/roles/sonarr ~/cloudbox_mod/roles/
   ```

1. Add Ansible role into cloudbox_mod.yml.

    ```bash
    nano ~/cloudbox_mod/cloudbox_mod.yml
    ```

    ```yaml
    ---
    - hosts: localhost
      vars_files:
        - settings.yml
        - /home/seed/cloudbox/settings.yml
      roles:
        - { role: sonarr, tags: ['sonarr'] }
    ```


1. Make edits to the Ansible role. 

   ```
   nano ~/cloudbox_mod/roles/sonarr/tasks/main.yml
   ```

1. Run the newly modded Ansible role:

    ```bash
    sudo ansible-playbook cloudbox_mod.yml --tags sonarr
    ```
