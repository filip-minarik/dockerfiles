FROM ubuntu:18.04

# Environment variables
ENV domain localhost
ENV LC_CTYPE C.UTF-8
# Setup scripts for LibreOffice Online
ADD ["./install_office.sh","./start_office.sh", "/usr/local/bin/"]
RUN bash /usr/local/bin/install_office.sh

EXPOSE 9980

# switch to lool user
USER 101

# Entry point
CMD bash /usr/local/bin/start-office.sh
