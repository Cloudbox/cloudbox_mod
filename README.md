# cloudbox_mod
Blank Template to add custom Ansible roles.

## How to use this template

1. Clone this repo:

    ```bash
    git clone https://github.com/Cloudbox/cloudbox_mod.git ~/cloudbox_mod
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
