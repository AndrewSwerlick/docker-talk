FROM ubuntu:14.04

# ==============================================================================
# Setting up base ubuntu environment
# ==============================================================================

# Ignore APT warnings about not having a TTY
ENV DEBIAN_FRONTEND noninteractive

# Ensure UTF-8 locale
RUN locale-gen en_US.UTF-8
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8
RUN dpkg-reconfigure locales

# Install build dependencies
RUN apt-get update -qq && \
    apt-get install -y -qq \
      build-essential \
      ca-certificates \
      curl \
      libcurl4-openssl-dev \
      libffi-dev \
      libgdbm-dev \
      libpq-dev \
      libreadline6-dev \
      libssl-dev \
      libtool \
      libxml2-dev \
      libxslt-dev \
      libyaml-dev \
      postgresql-client \
      software-properties-common \
      wget \
      git \
      libsqlite3-dev \
      sqlite3 \
      zlib1g-dev \
      libpq-dev \
      imagemagick \
      libmagickwand-dev \
      ghostscript \
      npm

## Brightbox Ruby 1.9.3, 2.0 and 2.1
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C3173AA6
RUN echo deb http://ppa.launchpad.net/brightbox/ruby-ng/ubuntu trusty main > /etc/apt/sources.list.d/brightbox.list

## Chris Lea's Node.js PPA
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C7917B12
RUN echo deb http://ppa.launchpad.net/chris-lea/node.js/ubuntu trusty main > /etc/apt/sources.list.d/nodejs.list

RUN apt-get update && apt-get install -y ruby2.1 ruby2.1-dev nodejs

# Install bundler
RUN gem2.1 install rake bundler --no-rdoc --no-ri

# Add options to gemrc
RUN echo "gem: --no-ri --no-rdoc" > /etc/gemrc

# Creating app user
RUN mkdir /home/app
RUN groupadd -r app -g 433 && \
useradd -u 431 -r -g app -d /home/app -s /sbin/nologin -c "Docker image user" app && \
chown -R app:app /home/app
