Folder with examples about how to use the project.

## Files

- Dockerfile

A dockerized debian image that creates a pyenv using the project.

Build the docker image:

~~~
docker build -t python_version .
~~~

Run the docker image:

~~~
docker run --name python_version_run --rm -it python_version
~~~


- run.md

Example of how to execute all available project options.
