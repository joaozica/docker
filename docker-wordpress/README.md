docker-wordpress
======================

Out-of-the-box Wordpress docker image

Obs
======================
Dependence of container [lamp-full](https://github.com/marcondesdddi/docker/tree/master/docker-lamp-full)

Usage
-----

To create the image `wordpress`, execute the following command on the docker-wordpress folder:

	docker build -t wordpress .

You can now push your new image to the registry:

	docker push wordpress


Running your Wordpress docker image
-----------------------------------

Start your image:

	docker run -d -p 80:80 wordpress

You can now start configuring your Wordpress container!