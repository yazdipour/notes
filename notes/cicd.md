# ci/cd


## Fastlane

```shell
fastlane init
# modify fastlane file
fastlane android deploy
```

## Heroku

https://dashboard.heroku.com/apps/githubx/deploy/heroku-container

```shell
heroku --version
heroku login
cd to Docker Dir
heroku container:login
heroku create //create random App
heroku container:push web --app (appname)
heroku open --app (appname)
```

https://dashboard.heroku.com/apps/githubx/deploy/heroku-git

```shell
heroku login
git init
heroku git:remote -a (appname)
git add .
git commit -m php
git push heroku master
```