### !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !!
###
### This repository is not maintained any more as its contents have been merged with https://github.com/akamai/akamai-docker (I am one of its main contributors)
###
### !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !! !!

# Akamai DevOps Environment

Environment setup for Akamai DevOps:

- Akamai CLI and all modules available
- Terraform + Akamai provider
- curl and httpie with EdgeGrid addons

## How to use it

To create a new environment:

```
docker run -it --name mylab lukaszczerpak/akamai-devops-labs
```

To return to already created environment:

```
docker start -i mylab
```

### Sandbox

> *Note: Credits go to Nick Le Mouton for his awesome blog post: <https://www.noodles.net.nz/2018/10/12/running-akamai-sandbox-in-docker-with-https/>*

Assuming you run a webserver locally on port 5000 and sandbox is exposed on port 9550:

- ensure you run docker with port mapping:
  ```
  docker run -it -p 9550:9550 --name mylab lukaszczerpak/akamai-devops-labs
  ```

- set up sandbox client to listen on address `0.0.0.0`:
  ```
  "sandboxServerInfo": {
    "secure": false,
    "port": 9550,
    "host": "0.0.0.0"
  },
  ```

- setup origin mapping using a special docker hostname:
  ```
  "originMappings": [
    {
      "from": "",
      "to": {
        "secure": false,
        "port": 5000,
        "host": "host.docker.internal"
      }
    }
  ],
  ```

### non-interactive sessions

The above use case assumes that user starts bash sessions and invokes commands inside of it. However, it's also possible to use this docker image to execute commands straight like on the following example:

```
❯ docker run -it --rm -p 9550:9550 -v $HOME/.edgerc:/root/.edgerc -v $(pwd)/sandbox:/cli/.akamai-cli/cache/sandbox-cli lukaszczerpak/akamai-devops-labs akamai sandbox list
Local sandboxes:

current  name      sandbox_id
-------  --------  ------------------------------------
YES      lczerpak  11111111-222-3333-4444-555555555555
```

This way, the container is immediately removed when the execution is complete. You can use path mount - like in the example above - to persist state across multiple commands invocations. The example above stores *sandbox-cli* local data in `$(pwd)/sandbox` subfolder so it's possible to operate on the same sandbox like in a single bash session.

## Build

```bash
docker build -t lukaszczerpak/akamai-devops-labs:YYYYmmddHH00 .
docker tag lukaszczerpak/akamai-devops-labs:YYYYmmddHH00 lukaszczerpak/akamai-devops-labs:latest
docker push lukaszczerpak/akamai-devops-labs
```

## License
[Apache License 2.0](LICENSE)
