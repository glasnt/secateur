# Secateur

Secateur is a web app that allows you to temporary block or mute a Twitter account, *and* all their followers.

It's hosted at https://secateur.app

People who want to use Secateur can either use the public app or, if their privacy and security needs necessitate it, they can run their own instance by following these instructions.

## Setting up your own environment.

Secateur is a Django web application built to be run in a docker environment along with a cache server (redis) and database server (postgres).

To run your own instance of Secateur, you need the following:

- recent versions of [https://docs.docker.com/install/](`docker`) and [https://docs.docker.com/compose/install/](`docker-compose`)
- credentials for the [Twitter Developer API](https://developer.twitter.com/)
  * This requires registring for a Developer API account, and then registering your application
  * Ensure you enable: "Allow this application to be used to sign in with Twitter"
  * Ensure you add "http://localhost:5000/complete/twitter/" as a Callback URL

If you have those, setting up your developer environment should be straightforward:

1. Clone this repository.
2. Copy `.env-template` to `.env` and add your Twitter API credentials.
3. Run `docker-compose up`.

That, actually, ought to be all there is to it. Once the docker containers are running, you can go to `http://localhost:5000` and hopefully see the Secateur home page. If your Twitter Developer API stuff is set up, you should be able to log in to your own Secateur environment.

Once you've logged in, you'll probably want to upgrade your account to be the superuser:

```$ docker-compose exec app ./manage.py promotesuperuser ${MY_TWITTER_ACCOUNT}```

While secateur is still young, you'll also need to manually allow your account access to use the Twitter API. To do so, you'll need to login to the admin, go to Secateur > Users, and check the box for your account under the "Is Twitter API Enabled?" heading.
