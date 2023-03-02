Role Name
=========

Installs and configure a basic gitlab omnibus install

Molecule
------------

Molecule is a tool to help testing, linting etc to ensure the role is fulfilling
some basic requirements.

To setup environment to run Molecule tests ensure python is installed on machine.

Create a virtualenv for your work:
```bash
    python3 -m venv /path/to/your/venv
```

Then we proceed to install the requirements for what we are using.
This is configured to require podman with how this is setup but you could use docker.
It would require changes in the `/molecule/default/molecule.yaml to use the docker driver.

```bash
    source /path/to/your/venv/bin/activate
    python3 -m pip install wheel
    python3 -m pip install molecule[lint,podman,ansible]
```

Next step ensure the container image used by tests exists build it.

```bash
    podman build . -t ubuntu:latest
```

Now we can test that Molecule can create the environment needed to test.

```bash
    molecule create
```

Then you can check that the container exists with:
```bash
    molecule list
```

To run linting `molecule lint` should show you the results

To run the fullsuite of tasks with molecule you can run the following command

```bash
    molecule test
```

This will then run linting and creating and testing to run the role and then destroy the environment after.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
    - hosts: servers
      vars_files:
        - vars/main.yaml
      roles:
         - { role: ergho.gitlab }
```
Then inside the vars_files you could use these for example.

```
    gitlab_external_url: "https://gl.example.org/"
    gitlab_edition: "gitlab-ee"
    gitlab_version: "15.8.3-ee.0"
```
There's also an actual example in the examples folder how this could actually be deployed
