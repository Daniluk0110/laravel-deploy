# HTML meta для SSL
 ```html
<meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests">
```
 


# GITLAB CI
```yml
stages:
  - build
  - deploy

cache:
  paths:
    - vendor/
    - node_modules/

project_build:
  stage: build
  only:
    - develop
    - tags
  script:
    - pwd
    - composer install
    - npm install
    - npm run build
    - chmod 755 -R storage
  artifacts:
    paths:
      - ./
    expire_in: 10 mins

test_deploy:
  stage: deploy
  only:
    - develop
  variables:
    HOST: "194.67.125.168"
    USER: "root"
    PASSWORD: "opdW3ku#vVtF"
    APP_PATH: "/var/www/cars"
    BACKUP_PATH: "/var/www/backup"
  script:
    - export SSHPASS=$PASSWORD
    - sshpass -e ssh $USER@$HOST -o stricthostkeychecking=no "
      rm -rf $BACKUP_PATH/*
      && cp -R $APP_PATH $BACKUP_PATH
      "
    - sshpass -e ssh $USER@$HOST -o stricthostkeychecking=no "
      rm -rf $APP_PATH/*
      "
    - sshpass -e scp -o stricthostkeychecking=no -r * $USER@$HOST:$APP_PATH
    - sshpass -e ssh $USER@$HOST -o stricthostkeychecking=no "
      cd $APP_PATH
      && rm -rf .env
      && touch .env
      && echo 'APP_NAME=\"$TEST_APP_NAME\"' >> .env
      && echo "APP_ENV=local" >> .env
      && echo "APP_KEY=" >> .env
      && echo "APP_DEBUG=true" >> .env
      && echo "APP_URL=194.67.125.168" >> .env
      && echo "APP_NAME=cars" >> .env
      && php artisan key:generate
      && cat .env
      && chown -R www-data:www-data storage/
      "

prod_deploy:
  stage: deploy
  only:
    - tags
  when: manual
  variables:
    HOST: "194.67.97.8"
    USER: "root"
    PASSWORD: "@EvXd7:b=#4y"
    APP_PATH: "/var/www/cars"
    BACKUP_PATH: "/var/www/backup"
  script:
    - export SSHPASS=$PASSWORD
    - sshpass -e ssh $USER@$HOST -o stricthostkeychecking=no "
      rm -rf $BACKUP_PATH/*
      && cp -R $APP_PATH $BACKUP_PATH
      "
    - sshpass -e ssh $USER@$HOST -o stricthostkeychecking=no "
      rm -rf $APP_PATH/*
      "
    - sshpass -e scp -o stricthostkeychecking=no -r * $USER@$HOST:$APP_PATH
    - sshpass -e ssh $USER@$HOST -o stricthostkeychecking=no "
      cd $APP_PATH
      && rm -rf .env
      && touch .env
      && echo 'APP_NAME=\"$PROD_APP_NAME\"' >> .env
      && echo "APP_ENV=prod" >> .env
      && echo "APP_KEY=" >> .env
      && echo "APP_DEBUG=false" >> .env
      && echo "APP_URL=https://site.ru" >> .env
      && echo "ASSET_URL=https://site.ru" >> .env
      && echo "APP_NAME=cars" >> .env
      && php artisan key:generate
      && cat .env
      && chown -R www-data:www-data storage/
      && php artisan migrate --force
      && php artisan db:seed
      && php artisan cache:clear
      && php artisan config:cache
      && php artisan route:cache
      "

```



