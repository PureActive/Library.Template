FROM ubuntu:18.04

ADD https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb packages-microsoft-prod.deb
RUN apt-get update

# Add bootstrapping dependencies that both mono and .NET Core/Powershell require.
RUN apt-get install -y gnupg ca-certificates software-properties-common

# mono (takes the longest, so put in the earlier layers)
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
RUN echo "deb https://download.mono-project.com/repo/ubuntu stable-bionic main" | tee /etc/apt/sources.list.d/mono-official-stable.list
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y mono-devel

# .NET Core and PowerShell prep
RUN dpkg -i packages-microsoft-prod.deb
RUN add-apt-repository universe
RUN apt-get update

# Other infrequently updated software
RUN apt-get install -y git apt-transport-https
RUN apt-get install -y powershell
RUN apt-get install -y dotnet-sdk-3.1

ADD https://dot.net/v1/dotnet-install.sh /tmp/dotnet-install.sh
RUN apt-get install -y curl
RUN chmod +x /tmp/dotnet-install.sh \
 && /tmp/dotnet-install.sh --install-dir /usr/share/dotnet -v 3.1.201 \
 && /tmp/dotnet-install.sh --install-dir /usr/share/dotnet -v 2.1.17 --runtime dotnet
