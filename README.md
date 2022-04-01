# Backend for the Screenplay Card Game - setup server


### 1. Prepare the remote (or local) server
Make sure the remote server has...
- installed jdk 11 or later.
- installed docker and docker-compose
- installed aws-cli 
- in the directory '.aws', register account credentials and config files. 
- has registered a domain name (comicogames.io) using namecheap for example
- you don't need to register the subdomain (prod.comicogames.io & test.comicogames.io) using duckdns for example. 

### 2. Set up directories
- Create swag directory: 'mkdir SwagDockerDir'
- Create a directory per branch: 'mkdir prodBranchDir' and 'mkdir testBranchDir'. 
- (or if you have different branch names, <yourbranchname>+Dir)

### 3. Set up nginx 
- Inside 'SwagDockerDir', place the file 'swag-docker-compose.yml' and rename to 'docker-compose.yml'
- Start swag for the first time: 'docker-compose build'
- This will create a directory named Dockervolumes. Under Dockervolumes/swagVolumes/nginx/site-confs, there is a file called default. Check that it contains a line saying include /config/nginx/proxy-confs/*.subdomain.conf;
  (Alternatively, you can replace this file with the file named 'default' of this repository)
- Place the files 'prod.subdomain.conf' and 'test.subdomain.conf' inside the directory Dockervolumes/swagVolumes/nginx/proxy-confs.

### 4. Check the following: 
- server-name in the ...conf files equal the subdomain we want to access, which is equal to the name of the file
- $upstream_app equals the name of the container created inside docker-compose of each branch
- $upstream_port equals the external port number mapped to the application port (6789) in docker-compose of each branch
- nothing is running on ports 6789(prod) and 6788(test)

### 5. Run
- Start the swag server: 'docker-compose up'
- Do any commit action on prodBranch and testBranch and wait for pipeline to run. 
