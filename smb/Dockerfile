# Use the base image with LAMP stack installed
FROM mattrayner/lamp:1404-php5-base

# Install wget and any other necessary packages
RUN apt-get update && \
    apt-get install -y wget

# Initialize MySQL data directory
RUN mysql_install_db --user=mysql --ldata=/var/lib/mysql

# Start MySQL and Apache services, and run the SIM Server installation script
RUN service mysql start && \
    service apache2 start && \
    sleep 5 && \
    cd /root && \
    wget http://47.242.36.50/update/smb_scheduler_install-latest.tar.gz && \
    tar -xzf smb_scheduler_install-latest.tar.gz && \
    cd smb_scheduler_install && \
    printf "\n\n\n" | ./smb_scheduler_install.sh

# Expose the required ports
EXPOSE 56012 56011/udp 80

# Start Apache and MySQL when the container starts
CMD ["sh", "-c", "service mysql start && service apache2 start && tail -F /dev/null"]