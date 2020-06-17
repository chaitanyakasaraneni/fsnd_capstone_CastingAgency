
# Casting Agency API

This project is backend web application following `Udacity Fullstack Developer Nanodegree` guidelines. It's a web app for a casting agency where users can add movies, actors, and relate each actor to the movies he/she acted in, and vice versa. This project uses python, flask and postgresql for it's backend and hosted on heruko. 

All backend code follows [PEP8 style guidelines](https://www.python.org/dev/peps/pep-0008/)

As of now, there is no frontend for this app. You can test it using cURL or [Postman](https://www.postman.com)

This app is deployed on heroku under this [link](https://fsnd-capstone-castingagency.herokuapp.com/).


## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)


#### Virtual Enviornment

I recommend working within a virtual environment whenever using Python for projects. This keeps dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for the platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)


#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.


## Running the server

First ensure you are working using your created virtual environment.

To run the server, execute:

```bash
source setup.sh
export FLASK_APP=app.py
export FLASK_ENV=development
flask run
```
Sourcing `setup.sh` sets some environment variables used by the app.

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `app.py` directs flask to use the this file to find the application.


## API Reference

### Getting Started

- Base URL: You can run this API locally at the default `http://127.0.0.1:5000/`
- Authentication: This app has 3 roles. Each role has its own token which are provided in `setup.sh` file. Details about each user privileges are provided below.

### Roles

This app has 3 Roles. Each role has its own privileges.

- Casting Assistant
	- Can view actors and movies
		- get:movies
		- get:actors

- Casting Director
	- All permissions a Casting Assistant has
		- get:movies
		- get:actors
	- Add or delete an actor from the database
		- post:actors
		- delete: actors
	- Modify actors or movies
		- patch:actors
		- patch:movies

- Executive Producer
	- All permissions a Casting Director has
		- get:movies
		- get:actors
		- post:actors
		- delete: actors
		- patch:actors
		- patch:movies
	- Add or delete a movie from the database
		- post:movies
		- delete:movie

Please Note, to use any endpoint, you must send the request with user access token in Authorization header, which are provided in `setup.sh`.



### Endpoints

- GET '/Actors'
- GET '/Movies'
- POST '/Actors'
- POST '/Movies'
- PATCH '/Actors/<id:int>'
- PATCH '/Movies/<id:int>'
- DELETE '/Actors/<id:int>'
- DELETE '/Movies/<id:int>'

Following is the sample response at each endpoint.

- GET '/Actors'
	- Fetch all Actor info from db
	- Request Argument : None
	- Returns : JSON response containing all actors with their info, and request status
	- example
		```
		{
		  "Actors": [
		    {
		      "age": 38,
		      "email": "Noha@gmail.com",
		      "id": 3,
		      "movies": [
		        "GoGo",
		        "alo"
		      ],
		      "name": "Noha",
		      "salary": 1000
		    }
		  ],
		  "success": true
		}
		```

- GET '/Movies'
	- Fetch all Movies info from db
	- Request Argument : None
	- Returns : JSON response containing all movies with their info, and request status
	- example
		```
		{
		  "Movies": [
		    {
		      "actors": [
		        "ALi",
		        "Ahmed"
		      ],
		      "genre": "Romance",
		      "id": 3,
		      "length": 1.9
		    }
		  ],
		  "success": true
		}
		```

- POST '/Actors'
	- Insert Actor info into db
	- Request Argument :  `name` `email` `age` `salary` `movie_ID`
	- Returns : JSON response containing request status
	- example
		```
		{
		  "success": true
		}
		```

- POST '/Movies'
	- Insert Movie info into db
	- Request Argument : `name` `length` `genre` `actor_ID`
	- Returns : JSON response containing request status
	- example
		```
		{
		  "success": true
		}
		```

- PATCH '/Actors/<int:id>'
	- Updtae Actor info and insert it db
	- Request Argument : `Actor id`  `name` `email` `age` `salary` 
	- Returns : JSON response containing request status
	- example
		```
		{
		  "success": true
		}
		```

- PATCH '/Movies/<int:id>'
	- Updtae Movie info and insert it db
	- Request Argument : `Movie id` `name` `length` `genre`
	- Returns : JSON response containing request status
	- example
		```
		{
		  "success": true
		}
		```

- DELETE '/Actors/<int:id>'
	- Delete Actor from db
	- Request Argument : Actor id
	- Returns : JSON response containing request status
	- example
		```
		{
		  "success": true
		}
		```

- DELETE '/Movies/<int:id>'
	- Delete Movie from db
	- Request Argument : Movie id
	- Returns : JSON response containing request status
	- example
		```
		{
		  "success": true
		}
		```

## Testing

To run the tests, run
```
dropdb capstone_test
createdb capstone_test
psql capstone_test < db.psql
python test_app.py
```

## Deployment

This app is deployed on heroku under this [link](https://fsnd-capstone-castingagency.herokuapp.com/).

