FROM ruby:2.7.6

# Set ARG & ENV variables.
ARG PROJECT_NAME
ENV env_project_name=$PROJECT_NAME

# Register Yarn package source.
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# Install additional packages.
RUN apt update -qq
RUN apt install -y postgresql-client nodejs yarn

# Prepare working directory.
WORKDIR /$env_project_name
COPY . /$env_project_name

# DOCKERFILE TODO: Copy & paste database.yml on config/database.yml
# This worked but did not copy it to my local file: ./config/database.yml
# COPY ./.docker/database.yml ./config/database.yml 
# COPY .env.docker /appname/.env
# END TODO

RUN gem install bundler
RUN bundle install

# DOCKERFILE TODO: Copy & paste database.yml on config/database.yml
# RUN ls
# RUN cp .docker/database.yml ./config/
# END TODO

# Configure endpoint.
COPY ./.docker/entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000

# Start app server.
CMD ["bundle", "exec", "rails", "server", "-b", "0.0.0.0"]
