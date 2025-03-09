FROM jenkins/jenkins:lts

ADD "https://www.random.org/cgi-bin/randbyte?nbytes=10&format=h" skipcache
USER root
RUN apt update

# tools
RUN apt install rsync -y
RUN apt install ansible -y
RUN apt install wget -y
RUN apt install pip -y
RUN wget https://releases.hashicorp.com/terraform/1.8.4/terraform_1.8.4_linux_amd64.zip -O /root/terraform.zip
RUN unzip /root/terraform.zip -d /root/
RUN mv /root/terraform /usr/local/bin/terraform
RUN rm -rf /root/terraform* /root/LICENSE.txt
RUN sh -c "$(curl https://get.docker.com)"
RUN curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose
COPY files/pip.conf /root/.config/pip/pip.conf
RUN cd /usr/local/bin && curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" 
RUN chmod +x /usr/local/bin/kubectl

COPY config/root/ssh/config /root/.ssh/config

RUN usermod -aG docker jenkins
