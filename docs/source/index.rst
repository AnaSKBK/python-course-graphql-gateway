GraphQL API Gateway
===================

GraphQL API шлюз для взаимодействия с микросервисами.

Зависимости
===========
Install the appropriate software:

Docker Desktop.
Git.
PyCharm (optional).


Установка
=========
Clone the repository to your computer:

git clone https://github.com/mnv/python-course-graphql-gateway
To configure the application copy .env.sample into .env file:

cp .env.sample .env
This file contains environment variables that will share their values across the application. The sample file (.env.sample) contains a set of variables with default values. So it can be configured depending on the environment.

Build the container using Docker Compose:

docker compose build
This command should be run from the root directory where Dockerfile is located. You also need to build the docker container again in case if you have updated requirements.txt.

To run the project inside the Docker container:

docker compose up
When containers are up server starts at http://0.0.0.0:8000/graphql. You can open it in your browser.


Использование
=============
Query example to request a list of favorite places:

query {
  places {
    latitude
    longitude
    description
    city
    locality
  }
}
Query example to request a list of favorite places with countries information:

query {
  places {
    latitude
    longitude
    description
    city
    locality
    country {
      name
      capital
      alpha2code
      alpha3code
      capital
      region
      subregion
      population
      latitude
      longitude
      demonym
      area
      numericCode
      flag
      currencies
      languages
    }
  }
}
Query example to get specific favorite place:

{
  place(placeId:1) {
    id
    latitude
    longitude
    description
    city
    locality
  }
}
Query example to create new favorite place:

mutation {
  createPlace (
    latitude: 25.20485,
    longitude: 55.27078,
    description: "Nice food."
  ) {
    place {
      id
      latitude
      longitude
      description
      city
      locality
    }
    result
  }
}
Query example to delete specific favorite place:

mutation {
  deletePlace(placeId: 1) {
    result
  }
}
Query example to create a favorite place:


This query will request additional information about related countries in optimal way using data loaders to prevent N + 1 requests problem.


Автоматизация
=============
The project contains a special Makefile that provides shortcuts for a set of commands:

Build the Docker container:

make build
Generate Sphinx documentation run:

make docs-html
Autoformat source code:

make format
Static analysis (linters):

make lint
Autotests:

make test
The test coverage report will be located at src/htmlcov/index.html. So you can estimate the quality of automated test coverage.

Run autoformat, linters and tests in one command:

make all
Run these commands from the source directory where Makefile is located.


Тестирование
============


