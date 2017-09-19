# docker-compose lamp stack sample template

A sample configuration of a lamp-stack development environment using docker-compose.

## getting startet

1. Download this repositories files
```
git clone --depth=1 --branch=master git@github.com:cioddi/docker_compose_lamp.git your_project_image_name

# remove the .git folder
rm -rf your_project_image_name/.git
```

2. Edit mysql/init.sql to create an initial database for your project
3. Add your preojects PHP files to this images folder. I prefer doing it as a git submodule.
```
git submodule add {path_to_the_git_repo}
```

4. Adjust the apache host config in php/hostconfig.conf and the mounted webroot (currently ./html) in docker-compose.yml to meet your projects needs.
  - You can specify a command that is supposed to run on container start inside the apache container at the "command" key of the php service defined in doccker-compose.yml.
5. Build and start the docker services defined in the docker-compose.yml file using the command ```docker-compose up -d --build```.
6. Browse to your php projects webroot on http://localhost:8000
7. Browse to PhpMyAdmin on http://localhost:8080 to inspect the database or import/export database data.

