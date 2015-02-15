FROM hermann/base-rails

WORKDIR /home/app

ADD Gemfile /home/app/
ADD Gemfile.lock /home/app/
RUN chown -R app:app /home/app

USER app
ENV HOME /home/app
# throw errors if Gemfile has been modified since Gemfile.lock
RUN bundle config frozen 1
RUN bundle install --deployment

USER root
WORKDIR /home/app
ADD . /home/app
RUN chown -R app:app /home/app

USER app
# have to set a fake secrete key while doing rake assets precomiple otherwise devise complains
RUN SECRET_KEY_BASE="dummy" RAILS_ENV=production bundle exec rake assets:precompile

USER root
# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

USER app
CMD ["bundle","exec","rails","server", "thin", "-b", "0.0.0.0"]

EXPOSE 3000
