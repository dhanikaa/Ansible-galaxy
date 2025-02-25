# Ansible Galaxy: Managing Roles and Uploading Custom Roles

## Introduction

Ansible Galaxy is a repository for Ansible roles that allows users to share and reuse automation code. With Ansible Galaxy, you can easily install pre-built roles from the community and publish your own roles for others to use.

This guide covers:
✅ How to install roles from Ansible Galaxy  
✅ Where Ansible Galaxy installs roles  
✅ Using a downloaded role in a playbook  
✅ How to publish your own role to Ansible Galaxy  
✅ Generating and using an API token for Ansible Galaxy  

---

## Installing Roles from Ansible Galaxy

To install a role from Ansible Galaxy, use the following command:

```sh
ansible-galaxy role install <role-name>
```

For example, to install the `bsmeding.docker` role, run:

```sh
ansible-galaxy role install bsmeding.docker
```

### Where Are Roles Installed?
By default, Ansible Galaxy installs roles in the following directory:

```sh
~/.ansible/roles/
```

You can verify the installed roles by listing the directory:

```sh
ls ~/.ansible/roles/
```

---

## Using an Installed Role in a Playbook

Once installed, you can use the role in an Ansible playbook. Here’s an example `docker-playbook.yaml` that uses the `bsmeding.docker` role:

```yaml
---
- hosts: all
  become: true
  roles:
    - bsmeding.docker
```

Run the playbook with:

```sh
ansible-playbook -i inventory.ini docker-playbook.yaml
```

---

## Publishing Your Own Role to Ansible Galaxy

If you want to share your own role on Ansible Galaxy, follow these steps:

### 1️⃣ Create a GitHub Repository for Your Role
Create a GitHub repository with a name following the format: `ansible-role-<role-name>` (e.g., `ansible-role-docker`).

### 2️⃣ Structure Your Role Properly
Your repository should have the following structure:

```
ansible-role-docker/
│-- defaults/       # Default variables
│-- files/          # Static files
│-- handlers/       # Handlers for services
│-- meta/           # Role metadata
│-- tasks/          # Task definitions
│-- templates/      # Jinja2 templates
│-- vars/           # Role-specific variables
│-- README.md       # Documentation
```

You can generate this structure using:

```sh
ansible-galaxy role init ansible-role-docker
```

### 3️⃣ Upload Your Role to GitHub
Push your role to GitHub:

```sh
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<your-github-username>/ansible-role-docker.git
git push -u origin main
```

### 4️⃣ Import the Role to Ansible Galaxy
To upload your role to Ansible Galaxy, use:

```sh
ansible-galaxy role import <github-username> <repo-name> --token <your-api-token>
```

For example:

```sh
ansible-galaxy role import myusername ansible-role-docker --token myapitoken123
```

---

## Getting an API Token for Ansible Galaxy

To upload a role, you need an API token from Ansible Galaxy. Follow these steps:

1. Go to [Ansible Galaxy](https://galaxy.ansible.com/)
2. Log in with your GitHub account.
3. Click on your profile and go to **API Tokens**.
4. Click **Create Token**.
5. Copy the generated token and use it in the `ansible-galaxy role import` command.

**Note:** Keep your API token secure and do not share it publicly.

---

## Additional Considerations

### Updating an Installed Role
To update an installed role, use:

```sh
ansible-galaxy role install <role-name> --force
```

For example:

```sh
ansible-galaxy role install bsmeding.docker --force
```

### Installing Roles from a Requirements File
You can install multiple roles using a `requirements.yml` file:

```yaml
- src: bsmeding.docker
- src: geerlingguy.nginx
```

Install all roles listed in the file with:

```sh
ansible-galaxy role install -r requirements.yml
```

---

## Conclusion

Ansible Galaxy simplifies role management by allowing users to install, share, and maintain reusable roles. By following this guide, you can:

✅ Install and use roles from Ansible Galaxy  
✅ Understand where roles are stored  
✅ Publish your own roles to Ansible Galaxy  
✅ Manage API tokens for authentication  

Start leveraging Ansible Galaxy today to streamline your automation workflows! 🚀