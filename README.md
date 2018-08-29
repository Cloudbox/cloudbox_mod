# cloudbox_mod
Blank Template to add custom Ansible roles to Cloudbox.

## How to use this template

1. Clone this repo:

    ```bash
    git clone https://github.com/Cloudbox/cloudbox_mod.git ~/cloudbox_mod
    ```

1. CD into the `cloudbox_mod` folder:

    ```bash
    cd ~/cloudbox_mod
    ```

1. If you have an Ansible vault password file, add the location to `ansible.cfg`:

    To edit:

    ```bash
    nano ~/cloudbox_mod/ansible.cfg
    ```

    Add line (with path to your vault password file):
    ```ini
    vault_password_file = ~/.ansible_vault
    ```

    Final result:
    ```ini
    [defaults]
    inventory = ~/cloudbox/inventories/local
    callback_whitelist = profile_tasks
    command_warnings = False
    retry_files_enabled = False
    hash_behaviour = merge
    role_path = ~/cloudbox/roles
    vault_password_file = ~/.ansible_vault
    ```

1. Create folders for the Ansible role:

    ```bash
    mkdir -p ~/cloudbox_mod/roles/newrole/tasks/
    ```

1. Place the task file there:

    ```bash
    touch ~/cloudbox_mod/roles/newrole/tasks/main.yml
    ```

1. Add custom variables into `settings.yml`:

    ```
    ~/cloudbox_mod/settings.yml
    ```


1. Add the Ansible role to `cloudbox_mod.yml`:

    To edit:

    ```bash
    nano ~/cloudbox_mod/cloudbox_mod.yml
    ```

    Add the following line under `roles:`:
    ```yaml
        - { role: newrole, tags: ['newrole'] }
    ```

    Final result:
    ```yaml
    ---
    - hosts: localhost
      vars_files:
        - settings.yml
        - ['~/cloudbox/accounts.yml', '~/cloudbox/accounts.yml.default']
        - ['~/cloudbox/settings.yml', '~/cloudbox/settings.yml.default']
        - ['~/cloudbox/adv_settings.yml', '~/cloudbox/adv_settings.yml.default']
      roles:
        - { role: pre_tasks }
        - { role: myrole, tags: ['myrole'] }
        - { role: newrole, tags: ['newrole'] }
    ```

    Note: The `pre_tasks` role is required and should not be removed.

1. Run the Ansible role:

    ```bash
    sudo ansible-playbook cloudbox_mod.yml --tags newrole
    ```
