FROM itsafeaturemythic/mythic_python_base:latest

# install .net core
RUN wget https://packages.microsoft.com/config/debian/10/packages-microsoft-prod.deb -O packages-microsoft-prod.deb && \
    dpkg -i packages-microsoft-prod.deb && \
    rm packages-microsoft-prod.deb

# install mono, protoc protobufs, and .net core
RUN apt-get -y update && \
    apt-get -y autoremove && \
    apt-get clean && \
    apt install --no-install-recommends -y apt-transport-https dirmngr gnupg ca-certificates && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && \
    echo "deb https://download.mono-project.com/repo/debian stable-buster main" | tee /etc/apt/sources.list.d/mono-official-stable.list && \
    apt update && apt-get install --no-install-recommends nuget \
    libreadline-dev llvm libncurses5-dev libncursesw5-dev mono-complete gcc-mingw-w64  -y && \
    wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh && \
    chmod +x dotnet-install.sh && \
    ./dotnet-install.sh --channel 7.0 && \
    rm dotnet-install.sh && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p "/Windows/assembly/GAC_MSIL/System.Management.Automation/1.0.0.0__31bf3856ad364e35"
COPY ["System.Management.Automation.dll", "/Windows/assembly/GAC_MSIL/System.Management.Automation/1.0.0.0__31bf3856ad364e35/System.Management.Automation.dll"]
RUN mkdir -p "/Windows/Microsoft.NET/assembly/GAC_MSIL/System.Management.Automation/v4.0_3.0.0.0__31bf3856ad364e35"
COPY ["System.Management.Automation.dll-v4", "/Windows/Microsoft.NET/assembly/GAC_MSIL/System.Management.Automation/v4.0_3.0.0.0__31bf3856ad364e35/System.Management.Automation.dll"]

# update the path to include the path to the dotnet isntall since it's different than normal
ENV PATH=/root/.dotnet:$PATH
ENV DOTNET_ROOT=/root/.dotnet/