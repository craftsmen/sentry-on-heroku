# Sentry on Heroku

## Setup guide

Follow the steps below to get Sentry up and running on Heroku:

1. Create a new Heroku application. Replace "APP_NAME" with your
   application's name:

        heroku apps:create APP_NAME

2. Add PostgresSQL to the application:

        heroku addons:create heroku-postgresql:hobby-dev

3. Add Redis to the application:

        heroku addons:create heroku-redis

4. Set Django's secret key for cryptographic signing and Sentry's shared secret
   for global administration privileges:

        heroku config:set SECRET_KEY=$(python -c "import base64, os; print(base64.b64encode(os.urandom(40)).decode())")

5. Set the absolute URL to the Sentry root directory. The URL should not include
   a trailing slash. Replace the URL below with your application's URL:

        heroku config:set SENTRY_URL_PREFIX=https://sentry-example.herokuapp.com

6. Deploy Sentry to Heroku:

        git push heroku master

7. Run Sentry's database migrations:

        heroku run "sentry --config=sentry.conf.py upgrade --noinput"

8. Create a user account for yourself:

        heroku run "sentry --config=sentry.conf.py createuser"

That's it!

## Email notifications

Follow the steps below, if you want to enable Sentry's email notifications:

1. Add either SendGrid or Mandrill add-on to your Heroku application:

        heroku addons:create sendgrid

2. Set the reply-to email address for outgoing mail:

        heroku config:set SERVER_EMAIL=sentry@example.com

## Upgrades

1. Run the following command to update the requirements:

        pip-contrib requirements.in

   If the `pip-contrib` package isn't available in your machine, install it with:

        pip install pip-tools

2. Deploy the Heroku app:

        git push heroku master

3. You might need to run migrations or update ENV variables, depending on Sentry's
   version you are upgrading to.
