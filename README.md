# spark-in-docker
This simple setup allows you to run a Spark master and Spark workers in Docker using Docker Compose.

The approach is a modified version of the following article on Medium, brought together under one repository for simplicity:

https://medium.com/@marcovillarreal_40011/creating-a-spark-standalone-cluster-with-docker-and-docker-compose-ba9d743a157f



The files have been updated to use a more recent version of Spark (2.4.0) and there has been some modification of the Dockerfiles, including basing all of them on the Ubuntu base image, for ease of management.


## Usage: ##

You will need to build the images locally before being able to use them, since they are not available on Docker Hub.  To do this, simply run the script: ```build-images.sh``` using BASH.

Run ```docker-compose up``` from the root of the repo to spin up a Spark master and two Spark workers.

To increase the number of workers, simply add additional entries to the ```docker-compose.yml``` file.