Role Name
=========

This role allows performing some actions (commit, push) that cannot be yet performed using the git module.

Requirements
------------

**git** must be installed on the host that will run the role.

Role Variables
--------------

The role allows to perform a clone or a pull for a git repository.

| *variable* | *description* | *default* |
|--------------|------------------------------------------------|-----------|
| git_action            | The action to perform, can be clone/push | no default |
| git_branch            | The branch to clone from/to push to | main |
| git_commit_message    | The commit message to set | no default |
| git_repo_url          | The HTTPS URL of the repository | no default |
| git_repo_email        | The email of the user (only for push action) | no default |
| git_repo_token        | The GitHub token to use for pushing/cloning repos | no default - Leave it empty or undefined to use SSH keys |
| git_repo_username     | The GitHub username to use when interacting with the repo| no default |
| git_working_dir       | The directory where the the repo should be cloned (clone action), or the folder that contains the cloned repository folder (push action) | ~ |


The role sets a fact, **git_repo_path** that contains the path of the cloned repo, for further use.

Example Playbook
----------------

Use this requirements.yml to setup your dependencies:

    ---
    collections:
      - community.general
    roles:
      - name: ansible-git-role
        src: https://github.com/kubealex/ansible-sushy-tools-podman.git

Sample usage with default settings:

    - hosts: my_host
      vars:
        git_branch: my_branch
        git_repo_url: "https://github.com/kubealex/my_repo.git"
        git_repo_email: "this_is@email.me"
        git_repo_token: "Supersecret"
        git_repo_username: "kubealex"
        git_working_dir: /path/to/folder

      tasks:
        - name: Include git role for push
          ansible.builtin.include_role:
            name: ansible-git-role
          vars:
            git_action: push
            git_commit_message: "This is a sample"


License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
