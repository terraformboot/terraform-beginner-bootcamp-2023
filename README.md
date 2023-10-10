# Terraform Beginner Bootcamp 2023

## Semantic Versioning :mage: :mage:

This project is going to utilize semantic versioning for its tagging.

[semver.org](https://semver.org/)

The general format: 

**MAJOR.MINOR.PATCH**, eg. `1.0.1`

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes

## Install the Terraform CLI

### Considerations with the Terraform CLI changes
The Terraform CLI installation instructions have changed due to gpg keyring changes. So we nedeed to refer latest install CLI instructions via Terraform Documentation and change the scripting for install.

[Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

### Considerations for Linux Distribution

This project us built against Ubuntu. 
Please consider checking your Linux Distribution and change accordingly to dristribution needs. 

[How To Check OS Version in Linux](https://www.cyberciti.biz/faq/how-to-check-os-version-in-linux-command-line/)

Example of checking OS version: 
```
$ cat /etc/os-release
PRETTY_NAME="Ubuntu 22.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-p
```

### Refactoring into Bash Scripts 

While fixing Terraform CLI gpg depreciation issue we notice that the bash scripts steps were a considerable amount more code so we decided to create a bash script to install the Terraform CLI. 

This bash script is located here: [./bin/install_terraform_cli](./bin/install_terraform-cli)

- This will keep the Gitpod Task File ([.gitpod.yml](gitpod.yml)) tidy. 
- This allow us an easier to debug and execute manually Terrafomr CLI install 
- This will allow better portability for other projects that need to install Terraform CLI

### Shebang Considerations

A Shebang (prounced Sha-bang) tells the bash script what program will interpert the script. 

ChatGPT recommended this format for bash: `#!/usr/bin/bash`

- For portability for different OS distributions
- Will search the user's PATH for bash executable

[Shebang](https://en.wikipedia.org/wiki/Shebang_(Unix))

### Execution Considerations 

When executing the bash script we can use `./` shorthand notation to execute the bash script.

eg. `./bin/install_terraform_cli`

If we are using a script in .gitpod.yml we need to point the script to a program to interpert it. 

eg. `source ./bin/install_terraform_cli`

### Linux Permissions

In order to make our bash scripts executable we need to change linux permissions for the fix to be executable at the user mode.

```sh
chmod u+x ./bin/install_terraform_cli
```

Alternatively:
```sh
chmod 744 ./bin/install_terraform_cli
```

[chmod](https://en.wikipedia.org/wiki/Chmod)

### Github Lifecycle (Before, Init, Command)

We need to be careful when using the init because it will not rerun if we restart an existing workspace. 

[Github Workspace Lifecycle](https://www.gitpod.io/docs/configure/workspaces/workspace-lifecycle)