--------------------------------------------------------------------------------------------------
Installing Docker on centos 7
    $ sudo yum install -y yum-utils   device-mapper-persistent-data   lvm2
    $ sudo yum-config-manager     --add-repo     https://download.docker.com/linux/centos/docker-ce.repo
    $ sudo yum-config-manager --enable docker-ce-edge
    $ sudo yum install docker-ce
    $ sudo systemctl start docker
    $ sudo docker run hello-world
    $ sudo groupadd docker
    $ sudo usermod -aG docker $USER
    $ systemctl enable docker
    $ systemctl status docker
    $ docker --version
Check if all required configurations are met for running docker on host machine using below steps
    $ curl https://raw.githubusercontent.com/docker/docker/master/contrib/check-config.sh > check-config.sh
    $ bash check-config.sh 
    $ sudo docker run --rm -it alpine ping -c4  localhost
Installing Docker Compose
    $ sudo curl -L https://github.com/docker/compose/releases/download/1.17.0-rc1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
    $ sudo chmod +x /usr/local/bin/docker-compose
    $ sudo docker-compose --version
Installing Dockermachine on Centos 7
    $ curl -L https://github.com/docker/machine/releases/download/v0.13.0/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine && chmod +x /tmp/docker-machine && sudo cp /tmp/docker-machine /usr/local/bin/docker-machine
    $ scripts=( docker-machine-prompt.bash docker-machine-wrapper.bash docker-machine.bash ); for i in "${scripts[@]}"; do sudo wget https://raw.githubusercontent.com/docker/machine/v0.13.0/contrib/completion/bash/${i} -P /etc/bash_completion.d; done

One liner to stop / remove all of Docker containers:
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
