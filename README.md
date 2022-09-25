# Docker envs

The .env file will be used by docker-compose to adjust the environment of the docker-compose command itself. This is useful for variable inside the yaml file that need to be expanded, or variables used by compose itself. For more on the latter, see the compose CLI variables docs.

Defining an env_file inside the yaml will take environment variables from the file and inject them into the container.

https://docs.docker.com/develop/dev-best-practices/
https://docs.docker.com/compose/environment-variables/


```
[docker-envs-service-a 2/3] RUN echo 'This is my token $TOKEN'
[docker-envs-service-a 3/3] RUN echo 'This is my pass $PASS'
[docker-envs-service-b 2/5] RUN echo "Oh dang look at that big dog"
[docker-envs-service-b 3/5] RUN echo "This is my token 1234abcd"
[docker-envs-service-b 4/5] RUN echo "And this is my key 1"
[docker-envs-service-b 5/5] RUN echo "Are we in production? $PRODUCTION"
```

```bash
docker-compose exec service-b bin/sh

/ # echo $ANIMAL

/ # echo $PRODUCTION
true
/ # echo $KEY
x12987afdk3e
```

```bash
docker-compose exec service-a bin/sh
/ # echo $TOKEN
a1b2c3d4e5
/ # echo $PASS
1234
```

Values in the shell take precedence over those specified in the `.env` file.

https://python-poetry.org/docs/configuration/#using-environment-variables
