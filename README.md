# docker_ssh_pytorch

FROM nvcr.io/nvidia/pytorch:23.07-py3

# Install OpenSSH server
RUN apt-get update && apt-get install -y openssh-server

# Create SSH directory and set root password (change password!)
RUN mkdir /var/run/sshd \
    && echo 'root:yourpassword' | chpasswd \
    && sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# Expose SSH port
EXPOSE 22

# Start SSH server and keep container running
CMD ["/usr/sbin/sshd", "-D"]
