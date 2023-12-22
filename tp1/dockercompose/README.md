# Docker compose

Créez un fichier docker-compose.yml :
```bash
	[esinck@rockerwan compose_test]$ cat docker-compose.yml 
	version: "3"
	
	services:
	  conteneur_nul:
	    image: debian
	    entrypoint: sleep 9999
	  conteneur_flopesque:
	    image: debian
	    entrypoint: sleep 9999
```

Lancez les deux conteneurs :
```bash
	[esinck@rockerwan compose_test]$ docker compose up -d
	[+] Running 3/3
	 ✔ conteneur_flopesque 1 layers [⣿]      0B/0B      Pulled                                                       3.3s 
	   ✔ bc0734b949dc Already exists                                                                                 0.0s 
	 ✔ conteneur_nul Pulled                                                                                          3.4s 
	[+] Running 3/3
	 ✔ Network compose_test_default                  Created                                                         0.2s 
	 ✔ Container compose_test-conteneur_flopesque-1  Started                                                         0.4s 
	 ✔ Container compose_test-conteneur_nul-1        Started
```
Vérifier que les deux conteneurs tournent :
```bash
	[esinck@rockerwan compose_test]$ docker ps
	CONTAINER ID   IMAGE     COMMAND        CREATED          STATUS          PORTS     NAMES
	3ab3e705752d   debian    "sleep 9999"   54 seconds ago   Up 52 seconds             compose_test-conteneur_nul-1
	8a18c05f4bf0   debian    "sleep 9999"   54 seconds ago   Up 52 seconds             compose_test-conteneur_flopesque-1
```

Pop un shell dans le conteneur :
```bash
	root@3ab3e705752d:/# ping conteneur_flopesque
	PING conteneur_flopesque (172.18.0.2) 56(84) bytes of data.
	64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=1 ttl=64 time=0.068 ms
	64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=2 ttl=64 time=0.032 ms
	64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=3 ttl=64 time=0.033 ms
	64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=4 ttl=64 time=0.039 ms
	^C
	--- conteneur_flopesque ping statistics ---
	4 packets transmitted, 4 received, 0% packet loss, time 3089ms
	rtt min/avg/max/mdev = 0.032/0.043/0.068/0.014 ms

```

