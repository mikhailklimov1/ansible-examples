To create a custom service I used podman on Rocky 8.8

1) Creat a container w host IP address:

$ podman container run -d -p 1080:80 -v /var/www101/:/usr/local/apache2/htdocs/:Z --name 'some_process_192.168.0.1' httpd:latest

2) Generate a systemd file:

$ podman generate systemd --name some_process_192.168.0.1 --files --new

3) Change filename:

$ mv container-some_process_192.168.0.1.service some_process@192.168.0.1.service

4) Stop and remove podman container:

$ podman container stop <id>

$ podman container rm <id>

5) Start, enable and verify a service (replace full_path w path to the working directory):

$ systemctl --user daemon-reload

$ systemctl --user enable --now <full_path>/some_process@192.168.0.1.service

$ systemctl --user list-units --type=service
