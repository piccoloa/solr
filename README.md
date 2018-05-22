Create remote repo on github:
https://github.com/piccoloa/solr

Open terminal:

    >     cd to ~/GitHub
    >     mkdir solr
    >     cd solr
    >     git clone https://github.com/piccoloa/solr

Open Atom editor and add project folder solr
Open terminal console in Atom to create .gitignore file and and clone official solr docker repo

    >touch .gitignore . #create file
    >git clone https://github.com/docker-solr/docke r-solr

Add docker-solr directory and all its contents to .gitignore file and other directories or files that you don't want public on github.

    >/docker-solr/*

In Atom terminal change to docker-solr/7.3 folder to run docker build . command to build solr 7.3 docker image

    >cd cd docker-solr/7.3
    #run docker command to build a 7.3 image with the tag named solr7.3
    >docker build . -t solr7.3


Create shell executable file with docker command for starting and running the container on the my-network (docker network) with the host name solr and container name solr7.3 sharing host port 8983:8983 and shared volume ~/user/Github/solr/solr.  solr admin dashboard will be viewable in browser on localhost:8983

	>docker run -d --rm --network my-network --hostname solr --name=solr -p 8983:8983 -v /Users/[user]/Github/solr/solr/documents:/home solr7.3

Enter solr container bash by running:

    >docker -ti exec solr /bin/bash
    #solr@solr:/opt/solr$

Create sh command to run docker script to launch solr container for use.

	>mkdir shell-commands
	>touch start_run_solr.sh

Add following scripts to start_run_solr.sh file

    #!/bin/bash

	docker run -d --rm --network my-network --hostname solr --name=solr -p 8983:8983 -v /Users/[user]/Github/solr/solr/documents:/home solr7.3 #line 3
	docker exec -ti solr /bin/bash

In terminal change permissions for file with:

	>chmod +x start_run_solr.sh


Start learning SolR from sources on [website.](http://lucene.apache.org/solr/resources.html)

To use executable to launch solr container run command below shell-commands folder

	>./start_run_solr.sh
