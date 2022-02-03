PROJECT NOTES

Dockerfile Notes:

-This dockerfile is a 'recipe' for building my docker image. 
-build essential = adds any dependencies needed to compile anything
-libpq-dev = allows communication to postgres

-ENV INSTALL_PATH /mobydick = the path where our app will be installed within the container
-RUN mkdir -p $INSTALL_PATH = makes it

-WORKDIR $INSTALL_PATH = every command that gets run under WORKDIR will be within the context of the install path

-Copy in the requirements file
-Do a pip install

-Copy all the source code from the mobydock folder into the docker image

-Set a volume for the static folder (will be used later by nginx)

-Run the gunicorn server



Requirements.txt:

-Has the latest version of Flask/gunicorn
-Use SQLAlchemy
-psycopg2 allows talking to postgres via SQLAlchemy
-flask-redis wraps the standard python redis library, making it easier to configure


app.py:

-Setup a custom logger, output it to standardout (lets docker handle all the logs in the right way)

	-create_app: silent=True protects against errors
	-two routes:
		-homepage: when feed button clicked, use lookup via SQLAlchemy to grab a random message. Message is passed to the template	
		-seed page: if seed is gone to, the db will be reset, loop through the 	messages, committed to the feedback model, then redirected back to the home page

docker-compose.yml:

-YML that gets turned into docker run commands
-Instructions:
	-docker-compose up
	-go to localhost:8000/seed
	-feed Moby