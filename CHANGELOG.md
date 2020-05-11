# Changelog

## 202005111200

- [fix] Sandbox CLI doesn't require explicit build, it's now listed on the `package-list.json` endpoint
- [improvement] removed `.git` folders to reduce image size

## 202003251200

- [fix] `cffi` package throws an error about missing `gcc`
- [improvement] ensure bash session always starts and all environment variables are properly initialized. This improves compatibility to use this image in scripts (more details in README.md).

## 202002041100

- [new] AKAMAI_CLI_HOME is now configurable and defaults to "/cli"

## 202002032000

- [fix] fixed CLI wrapper build steps
- [new] EdgeWorkers CLI
- [update] updated Terraform to 0.12.20
- [update] all CLIs updated to the latest versions

## 201909061915

- [fix] missing dependency for Akamai Sandbox (<https://github.com/lukaszczerpak/akamai-devops-docker/issues/1>)
- [update] updated Terraform to 0.12.8

## 201908181000
- [update] updated Terraform to 0.12.6 with Akamai provider builtin

## 201903151200
- [new] added project page to the welcome message

## 201903071200
- [update] updated all CLIs to the latest versions

## 201902061800
- [new] added cli-sandbox (<https://github.com/akamai/cli-sandbox>)
- [update] updated all CLIs to the latest versions
