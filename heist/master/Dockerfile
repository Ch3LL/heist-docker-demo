FROM ubuntu:18.04

RUN apt-get update && apt-get install -y openssh-server python3-pip vim less
RUN mkdir /var/run/sshd
RUN echo 'root:toor' | chpasswd
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

RUN pip3 install heist pop rend PyYAML asyncssh jinja2 toml aiohttp salt
RUN mkdir -p /etc/heist/rosters
RUN mkdir -p /var/lib/heist/artifacts/linux/
COPY ./roster.cfg /etc/heist/rosters/


EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
