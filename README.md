Ansible role: chezmoi
=====================

Install and configure chezmoi for managing dotfiles.

Role Variables
--------------

```
ENTRY POINT: *main* - Install and configure chezmoi for managing dotfiles

Options (= indicates it is required):

- chezmoi_arch_map  Mapping of the possible values of
                     ansible_architecture to the chezmoi package
                     architectures
          default: null
          type: dict

- chezmoi_github_org  Name of organisation for chezmoi github
                       repository
          default: twpayne
          type: str

- chezmoi_github_repo  Name of chezmoi github repository
          default: chezmoi
          type: str

- chezmoi_github_token  Optional bearer token to use to authenticate
                         with api.github.com
          default: ''
          type: str

- chezmoi_init_apply  If true, run chezmoi apply when initialising a
                       chezmoi repo
          default: true
          type: bool

- chezmoi_init_args  Extra arguments to use when initialising a
                      chezmoi repo
          default: ''
          type: str

- chezmoi_install  If true, install chezmoi
          default: true
          type: bool

- chezmoi_repo_update_args  Extra arguments to use when updating a
                             chezmoi repo
          default: ''
          type: str

- chezmoi_repo_update_randomized_delay  Delay the chezmoi repo update
                                         timer by a random time up to
                                         this value or empty string
                                         for no delay
          default: 6h
          type: str

- chezmoi_repo_update_time  How often to update a users chezmoi repo,
                             accepts a systemd time, see
                             https://www.freedesktop.org/software/systemd/man/latest/systemd.time.html,
                             or "never"
          default: daily
          type: str

- chezmoi_update_randomized_delay  Delay the chezmoi update timer by
                                    a random time up to this value or
                                    empty string for no delay
          default: 6h
          type: str

- chezmoi_update_time  How often to update chezmoi, accepts a systemd
                        time, see
                        https://www.freedesktop.org/software/systemd/man/latest/systemd.time.html,
                        or "never"
          default: daily
          type: str

- chezmoi_users  List of user accounts to manage dotfiles for
          default: []
          elements: dict
          type: list
          options:

          - prompts  Answers for chezmoi prompts
            default: null
            type: dict
            options:

            - bool  Boolean answers
              default: null
              elements: dict
              type: list
              options:

              = key  Prompt name
                type: str

              = value  Prompt value
                type: str

            - choice  Choice answers
              default: null
              elements: dict
              type: list
              options:

              = key  Prompt name
                type: str

              = value  Prompt value
                type: str

            - multichoice  Multichoice answers
              default: null
              elements: dict
              type: list
              options:

              = key  Prompt name
                type: str

              = value  Prompt value
                type: str

            - string  String answers
              default: null
              elements: dict
              type: list
              options:

              = key  Prompt name
                type: str

              = value  Prompt value
                type: str

          = repo  Location of the users dotfile repo
            type: str

          = username  Name of the user account
            type: str

- chezmoi_version  Version to install (use "latest" for the latest
                    version)
          default: latest
          type: str
```

Installation
------------

This role can either be installed manually with the ansible-galaxy CLI tool:

    ansible-galaxy install git+https://github.com/wandansible/chezmoi,main,wandansible.chezmoi

Or, by adding the following to `requirements.yml`:

    - name: wandansible.chezmoi
      src: https://github.com/wandansible/chezmoi

Roles listed in `requirements.yml` can be installed with the following ansible-galaxy command:

    ansible-galaxy install -r requirements.yml

Example Playbook
----------------

    - hosts: all
      roles:
         - role: wandansible.chezmoi
           become: true
           vars:
             chezmoi_users:
               - username: example
                 repo: https://github.com/example/dotfiles
                 prompts:
                   string:
                     - key: email
                       value: user@example.org
