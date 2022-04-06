FROM ruby

# Install needed packages
RUN apt-get update && apt-get install -y --no-install-recommends && apt-get update && apt-get install -y mariadb-client postgresql-client sqlite3 --no-install-recommends

RUN mkdir -p /opt/app
WORKDIR /opt/app

ONBUILD COPY ./rails_app /opt/app/


# An ONBUILD command executes after the current Dockerfile build completes when the parent image is called
ONBUILD RUN bundler install
ONBUILD RUN bundle exec rake db:migrate
ONBUILD RUN bundle exec rake db:seed
#docker build -t ft-rails:on-build .
#docker run -it --rm ft-rails:on-build