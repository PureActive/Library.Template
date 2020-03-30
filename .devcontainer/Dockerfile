FROM ubuntu:19.10

ADD https://packages.microsoft.com/config/ubuntu/19.10/packages-microsoft-prod.deb packages-microsoft-prod.deb
RUN apt-get update && \
    apt-get install -y ca-certificates && \
    dpkg -i packages-microsoft-prod.deb && \
    apt-get update && \
    apt-get install -y apt-transport-https && \
    apt-get update && \
    apt-get install -y dotnet-sdk-3.1 git
