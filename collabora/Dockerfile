FROM ubuntu:18.04

# Environment variables
ENV domain localhost
ENV LC_CTYPE C.UTF-8

# Setup scripts for LibreOffice Online
ADD /scripts/install-office.sh /
ADD /scripts/start-office.sh /
RUN bash install-office.sh

EXPOSE 9980

# switch to lool user
USER 101

# Entry point
CMD bash start-office.sh
