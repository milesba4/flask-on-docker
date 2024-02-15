#


## Overview
This repository is a prepackaged implementation of dockerizing a flask application that uses services like Nginx and Gunicorn. The application created was a simple web app with static and media file upload capabilities. Listed below is a visual display of the web app, and the build instructions for replicating the results.

## Display (GIF)
![Dexter upload](https://recordit.co/gNc66Y0H53.gif)

## Build Instructions


### Development
1. Rename `.env.dev_example` to `.env.dev.` :

```
$ mv .env.dev_example .env.dev.
```
2. Build the production images and spin up the containers

```
$ docker-compose -f docker-compose.prod.yml up -d --build
$ docker-compose -f docker-compose.prod.yml exec web python manage.py create_db
```
Now, test this out by navigating to [](http://localhost:1336) 
 
### Production
*This makes use of the services Nginx and Gunicorn*

1. Rename `.env.dev.prod_example` to `.env.dev.prod` and rename `.env.dev.prod.db_example` to `.env.dev.prod.db`:

```
$ mv env.dev.prod_example .env.dev.prod
```

```
$ mv env.dev.prod.db_example .env.dev.prod.db
```
 *Customize their respective environmental variables used to access the postgres database*

2. Bring down containers, rebuild the production images and spin up the containers

```
$ docker-compose -f docker-compose.prod.yml down -v
$ docker-compose -f docker-compose.prod.yml up -d --build
$ docker-compose -f docker-compose.prod.yml exec web python manage.py create_db
```

### Testing 

Upload an image and navigate to this page on your browser (firefox reccomended) : [](http://localhost:1336/upload)

After uploading your file, navigate to this page on your browser to view the uploaded image: [](http://localhost:1336/media/IMAGE_FILE_NAME) (replace 'IMAGE_FILE_NAME' with name of uploaded image)




