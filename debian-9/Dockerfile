FROM python:3.7-slim-stretch

RUN apt-get update && apt-get install -y \
    curl \
    apt-transport-https \
    make \
    build-essential \
    unixodbc \
    unixodbc-dev \
    gnupg2 \
    tzdata \
    xvfb \
    xfonts-100dpi \
    xfonts-75dpi \
    xfonts-scalable \
    xfonts-cyrillic \
    wkhtmltopdf

RUN ln -fs /usr/share/zoneinfo/America/Fortaleza /etc/localtime && dpkg-reconfigure -f noninteractive tzdata
RUN LANG=pt_BR.UTF-8
RUN pip install --upgrade pip

RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list
RUN apt-get update
RUN ACCEPT_EULA=Y apt-get install msodbcsql17 mssql-tools -y
RUN echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
RUN echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc

RUN echo "---> Cleaning up" \
 && apt-get autoremove -y \
 && apt-get autoclean -y \
 && apt-get clean -y \
 && rm -rf /tmp/*

WORKDIR /application
