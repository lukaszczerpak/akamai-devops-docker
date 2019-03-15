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

## Build

```bash
docker build -t lukaszczerpak/akamai-devops-labs:YYYYmmddHH00 .
docker tag lukaszczerpak/akamai-devops-labs:YYYYmmddHH00 lukaszczerpak/akamai-devops-labs:latest
docker push lukaszczerpak/akamai-devops-labs
```

## License
[Apache License 2.0](LICENSE)
