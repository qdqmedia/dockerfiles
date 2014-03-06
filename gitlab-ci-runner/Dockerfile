# gitlab-ci-runner

from        ubuntu:12.04
maintainer  weisjohn "weis.john@gmail.com"


# add deadsnake ppa
run         apt-add-repository -y ppa:fkrull/deadsnakes

# apt-get deps

run         apt-get update -y
run         apt-get install -y -q sudo 
run         apt-get install -y -q wget 
run         apt-get install -y -q git 
run         apt-get install -y -q build-essential 
run         apt-get install -y -q libicu-dev
run         apt-get install -y -q python-pip
run         apt-get install -y -q python3.3 python2.7 python2.6 python2.5 python2.4 python3.3-dev python2.7-dev python2.6-dev python2.5-dev python2.4-dev



# install ruby 1.9.3, bundler

run         wget -O ruby-install-0.1.4.tar.gz https://github.com/postmodern/ruby-install/archive/v0.1.4.tar.gz
run         tar -xzvf ruby-install-0.1.4.tar.gz
run         ruby-install-0.1.4/bin/ruby-install -i /usr/local/ ruby 1.9.3 
run         rm -rf ruby-install-0.1.4/ ruby-install-0.1.4.tar.gz
run         gem install bundler



## install gitlab-ci-runner into /gcr

run         git clone https://github.com/Ensequence/gitlab-ci-runner.git gcr && cd gcr
run         cd gcr && bundle install 


# install python related tools
run         pip install tox coverage

# setup ssh 

## sub-optimal... it seems that ssh-keygen doesn't honor $HOME
## mkdir for .ssh keys in the base director
run         mkdir /.ssh
## modify ssh config to use the appropriate key 
run         echo "\nIdentityFile /.ssh/id_rsa" >> /etc/ssh/ssh_config


## the default command to be run when this docker image is started
cmd         /gcr/bin/runner