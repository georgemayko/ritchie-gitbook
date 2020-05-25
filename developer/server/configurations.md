# Configurations



{% hint style="info" %}
In the **Team version**, the ritchie-server repository provides the settings for the CLI. 

All the intelligence is in the CLI, and the information the CLI needs to function is provided by the server through that repository. 

**Each team** needs to have a configuration file to start their server when using Ritchie. That file is **file\_config.json**.
{% endhint %}

## Server configuration

The file\_config.json will contain the configuration and authorization part of the trees and commands, this involves the following fields: 

* name \(of the organization\) 
* keycloak 
* cliVersionPath 
* repositories 
* oauth 
* credentials

The _**name**_ field represents the organization that must be informed by the user when logging in with Ritchie in the Team version.

The _**keycloak**_ field refers to the [Keycloak](https://www.keycloak.org/) settings \(url, realm, clientId and clientSecret\). 

The _**cliVersionPath**_ field tells you the URL that the server uses to find out the current version of the CLI. 

The _**repositories**_ field indicates the formula repositories accessible by the team, and contains the URLs that the CLI will use to download the tree.json that will be in the [.rit folder ](../cli/.rit-folder.md)

The _**oauth**_ field contains the URL that will be used to login with the organization's SSO \(Single Sign On\) tool. 

The _**credentials**_ field contains a list of credentials that can be configured within the organization's environment, which can be set by both users and server administrators \(for specific users, or for the entire organization\).

### Here is an example of a file\_config.json

```text
{
  "zup": {
    "keycloak": {
      "url": "http://localhost:8080",
      "realm": "ritchie",
      "clientId": "user-login",
      "clientSecret": "user-login"
    },
    "cliVersionPath": {
      "provider": "s3",
      "url": "http://localhost:8882/s3-version-mock"
    },
    "repositories":
     [
       {
         "name": "commons",
         "priority": 0,
         "treePath": "/tree/tree.json",
         "remote" : "http://localhost:8882",
         "serverUrl" : "http://localhost:3000",
         "replaceRepoUrl" : "http://localhost:3000/formulas"
       },
       {
         "name": "zup",
         "priority": 1,
         "treePath": "/tree/tree-zup.json",
         "remote" : "http://localhost:8882",
         "serverUrl" : "http://localhost:3000",
         "replaceRepoUrl" : "http://localhost:3000/formulas"
       }
     ],

    "oauth" :{
      "url" : "http://localhost:8080/auth/realms/ritchie",
      "clientId" : "oauth"
    },
    "credentials": {
      "github": [
        {
          "field": "username",
          "type": "text"
        },
        {
          "field": "token",
          "type": "password"
        }
      ],
      "gitlab": [
        {
          "field": "username",
          "type": "text"
        },
        {
          "field": "token",
          "type": "password"
        }
      ],
      "email-zup": [
        {
          "field": "email",
          "type": "text"
        },
        {
          "field": "token",
          "type": "password"
        }
      ]
    }
  }
}
```

## Server testing

For the Team version to work on the CLI, the organization will need to move up: 

* a server 
* a [Keycloak](https://www.keycloak.org/) account \(open source tool\) 
* a [Vault](https://www.vaultproject.io/) account \(open source tool\) 

It is possible to test these settings locally, observing through Postman files \(available in the **/testdata** folder\) how the server endpoints are handled by the CLI to work. 

To start this test you need to run the file run-local.sh ****: `$ sh run-local.sh`

```text
#!/bin/bash

./create-vault-approle.sh . http://0.0.0.0:8200

export VAULT_ADDR=http://localhost:8200
export VAULT_AUTHENTICATION=APPROLE
export VAULT_ROLE_ID=$(cat /tmp/vault/role-id.txt)
export VAULT_SECRET_ID=$(cat /tmp/vault/secret-id.txt)
export FILE_CONFIG="$(pwd)/server/resources/file_config_local.json"

go run server/cmd/server/main.go
```

As well as running the repository **docker-compose** file : `$ docker-compose up`

```text
version: '3'

services:
  vault:
    image: vault:1.3.0
    ports:
      - "8200:8200"
    volumes:
      - ./resources/vault.hcl:/vault/config/vault.hcl
    environment:
      - VAULT_DEV_ROOT_TOKEN_ID=87e7784b-d598-44fe-8962-c7c345a11eed
      - VAULT_DEV_LISTEN_ADDRESS=0.0.0.0:8200
      - SKIP_SETCAP=true
      - disable_mlock=true

  keycloak:
    image: jboss/keycloak:7.0.0
    environment:
      DB_VENDOR: H2
      KEYCLOAK_IMPORT: /tmp/keycloak/ritchie.json
      KEYCLOAK_USER: admin
      KEYCLOAK_PASSWORD: admin
    ports:
      - "8080:8080"
    volumes:
      - ./testdata/security/keycloak:/tmp/keycloak

  stubby4j:
    image: sandokandias/stubby4j-docker
    ports:
      - "8787:8787"
      - "8882:8882"
    environment:
      STUBBY_PORT: 8882
    volumes:
      - ./testdata/stubby4j/integrations.yml:/usr/local/stubby.yml
      - ./testdata/stubby4j/response.zip:/usr/local/response.zip
```

These 2 files work together with the file\_config-local.json located in the /server/resources folder of the ritchie-server repository. 

Once everything is up, it will be possible to execute the requests via Postman that the CLI sends to the server to get the information necessary for its operation.

{% hint style="warning" %}
A core command is being developed to allow a team to be able to create the configuration files as soon as the realm in kubectl, to be able to generate a server already working with Ritchie in a simplified way.
{% endhint %}
