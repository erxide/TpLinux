# Image publique

Recuperez des images :
```bash
	[esinck@rockerwan ~]$ docker images
	REPOSITORY           TAG       IMAGE ID       CREATED        SIZE
	linuxserver/wikijs   latest    869729f6d3c5   6 days ago     441MB
	mysql                5.7       5107333e08a8   9 days ago     501MB
	python               latest    fc7a60e86bae   13 days ago    1.02GB
	wordpress            latest    fd2f5a0c6fba   2 weeks ago    739MB
	python               3.11      22140cbb3b0c   2 weeks ago    1.01GB
```

Lancez un conteneur à partir de l'image Python :
```bash
	[esinck@rockerwan ~]$ docker run -it python:3.11 bash
	root@2791aa567fea:/# python --version
	Python 3.11.7
```

# Construire une image :

Ecrire un Dockerfile pour une image qui héberge une application Python :

```bash
	FROM debian:bullseye-slim

	RUN apt update -y 

	RUN apt install -y python3 python3-pip

	RUN python3 -m pip install emoji

	WORKDIR /app

	COPY app.py /app

	ENTRYPOINT ["python3", "app.py"]
```

Build l'image :
```bash
	[esinck@rockerwan python_app_build]$ docker images
	REPOSITORY           TAG              IMAGE ID       CREATED         SIZE
	python_app           version_de_fou   4d82eb808bc7   3 minutes ago   441MB
```

Lancer l'image :
```bash
	[esinck@rockerwan python_app_build]$ docker run python_app:version_de_fou
	Cet exemple d'application est vraiment naze 👎
```

