# Docker Cheatsheet
This README provides some helpful stuff about [Docker](https://www.docker.com/).

## Setup

### Installing under CentOS
Setup the Docker repository:
```bash
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```
Install the Docker packages:
```bash
sudo yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```
Start the Docker engine:
```bash
sudo systemctl start docker
```
See [this link](https://docs.docker.com/engine/install/centos/) for more details.

### Allow non-root users run Docker CLI
Add the current user to the `docker` group:
```bash
sudo gpasswd -a $USER docker
```
Login/logout to activate the changes.

### Changing the Docker Data Root
Create (or edit) `/etc/docker/daemon.json`:
```
{
"data-root": "/path/to/new/docker_data_root"
}
```
Restart Docker:
```bash
sudo systemctl restart docker
```


## Running

### Running a command interactively
```bash
docker run -it --rm -v /dir/on/host:/dir/in/container:ro image command
```

### Bash script to check if an image exists
```bash
image="my_docker_image"
if [[ "$(docker images -q $image 2> /dev/null)" == "" ]]; then
    echo "Docker image $image does not (yet) exist"
    exit 1
fi
```
