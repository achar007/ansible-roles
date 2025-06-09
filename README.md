# Ansible Role Demo: my_webserver_role

This demo shows how to create and use an Ansible role to deploy and manage an Nginx web server, as well as how to roll back the changes.

## 1. Create the Role Structure

Initialize the role using Ansible Galaxy:

```bash
ansible-galaxy role init my_webserver_role
```

This creates the following structure:

```
my_webserver_role/
├── defaults/
│   └── main.yml
├── files/
│   └── index.html
├── handlers/
│   └── main.yml
├── meta/
│   └── main.yml
├── README.md
├── tasks/
│   └── main.yml
├── templates/
│   └── nginx.conf.j2
└── vars/
    └── main.yml
```

## 2. Deploy the Web Server

Run the playbook to deploy Nginx and your web content:

```bash
ansible-playbook site.yml
```

### Example Output

```
PLAY [home-lab1] ...
TASK [my_webserver_role : Ensure apt cache is updated] ...
TASK [my_webserver_role : Install nginx] ...
TASK [my_webserver_role : Deploy index.html] ...
TASK [my_webserver_role : Deploy nginx config] ...
TASK [my_webserver_role : Ensure nginx is running] ...
RUNNING HANDLER [my_webserver_role : Restart Nginx] ...
PLAY RECAP ...
```

## 3. Rollback (Uninstall Nginx and Clean Up)

To remove Nginx and clean up files, run:

```bash
ansible-playbook rollback.yml
```

### Example Output

```
PLAY [home-lab1] ...
TASK [Stop and disable nginx] ...
TASK [Remove nginx package] ...
TASK [Delete index.html] ...
TASK [Remove nginx config] ...
TASK [Clean apt cache] ...
PLAY RECAP ...
```

## 4. Files Overview
- `site.yml`: Main playbook to deploy the web server.
- `rollback.yml`: Playbook to remove Nginx and clean up.
- `my_webserver_role/`: Contains all role files (tasks, handlers, templates, etc).

## 5. Customization
- Edit `files/index.html` to change the web page content.
- Edit `templates/nginx.conf.j2` for custom Nginx configuration.

---

**This demo provides a simple, repeatable way to manage a web server using Ansible roles.**
