# GraphQL API Authorization with OPA

This directory helps provide fine-grained, policy-based control over who
can run which GraphQL API queries.

A [matching tutorial is available](https://www.openpolicyagent.org/docs/latest/graphql-api-authorization/).

## Contents

* A sample GraphQL application that asks OPA for authorization before executing a query (`docker/`)
* A default policy that allows `salary` queries for `<user>` and for `<user>`'s manager (`docker/policy`)
    * There are two policies given. The first is `example.rego` (and additionally, `example-hr.rego` from the tutorial),
      which is the default policy. The second is `example-jwt.rego`, which allows you to perform the same task, but
      by communicating information relevant to the policy via JSON Web Tokens. The tokens to use for the second
      policy can be found in the `tokens` directory. Files with the `jwt` extension are the tokens themselves, and
      files with the `txt` extension are their respective decoded tokens for reference.
    * Policies are provided to OPA in the form of bundles, where a simple Nginx server acts as a bundle server in
      the docker compose environment.

## Setup

Download the [latest opa binary](https://www.openpolicyagent.org/docs/latest/#running-opa) for your platform. 

For arm64 based macos:
```bash
curl -L -o /usr/local/bin/opa https://github.com/open-policy-agent/opa/releases/download/v0.46.1/opa_darwin_arm64_static
chmod 755 /usr/local/bin/opa
```

The GraphQL application, the bundle server, and OPA all run in docker-containers.
For convenience, we included a docker-compose file, so you'll want
[docker-compose](https://docs.docker.com/compose/install/) installed.

Note that if using Docker Desktop, you may instead use the `docker compose` command.

To build the containers and get them started, use the following make commands.

```
make       # build the containers with docker
make up    # start the containers with docker-compose
```

To instead use the example with JSON Web Tokens, use the following make commands.

```
make             # build the containers with docker
make up-token    # start the containers with docker-compose
```
