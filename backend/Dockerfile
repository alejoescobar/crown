FROM ruby:2.6.4-buster

RUN echo "deb http://deb.debian.org/debian jessie main" > /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y build-essential checkinstall libssl-dev
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.35.1/install.sh | bash
SHELL ["/bin/bash", "--login", "-c"]
RUN nvm install 14.3.0
RUN npm i -g yarn
RUN gem install bundler -v 2.1.4

RUN mkdir /crown
WORKDIR /crown
COPY Gemfile /crown/Gemfile
COPY Gemfile.lock /crown/Gemfile.lock
RUN bundle install
COPY . /crown
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000
CMD ["rails", "server", "-b", "0.0.0.0"]
