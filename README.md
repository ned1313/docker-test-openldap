# OpenLDAP Docker Image for testing

This image provides an OpenLDAP Server for testing the LDAPjs client. The server
is initialized with the example domain `globomantics.local` with data from the
[Futurama Wiki][futuramawikia]. The original code is from
[rroemhild/docker-test-openldap][rroemhild].

[futuramawikia]: http://futurama.wikia.com
[rroemhild]: https://github.com/rroemhild/docker-test-openldap

## Usage

Start the container in a terminal:

```sh
$ docker run --rm -it \
  -p 1389:389 \
  -p 1636:636 \
  ghcr.io/ldapjs/docker-test-openldap/openldap:latest
```

> Note: instead of `--it` you could use `-d` to start the container in the
> background.

Using your LDAP browser of choice, e.g. [Apache Directory Studio][ads], create
a connection profile with the following details:

1. Host: `127.0.0.1`
1. Port: `1389`
1. Bind DN: `cn=admin,dc=globomantics,dc=local`
1. Bind Password: `GoodNewsEveryone`

Connect via the profile and you can now browse all of the included test
data.

[ads]: https://directory.apache.org/studio/

## Building Locally

A build script, [`build-image.sh`](./build-image.sh), is included that will
build and push the images to the GitHub registry. You should not need to run
this script. For a local build, issue the following from the root directory
of this project:

```sh
$ docker build -t openldap .
```

The result will be a Docker image built for the local system's architecture
and stored in the local Docker image list. Running said image would look like:

```sh
$ docker run --rm -it -p 1389:389 openldap
```

## LDAP structure

### dc=globomantics,dc=local

| Admin            | Secret           |
| ---------------- | ---------------- |
| cn=admin,dc=globomantics,dc=local | GoodNewsEveryone |

### ou=people,dc=globomantics,dc=local

#### cn=Hubert J. Farnsworth,ou=people,dc=globomantics,dc=local

| Attribute        | Value            |
| ---------------- | ---------------- |
| objectClass      | inetOrgPerson |
| cn               | Hubert J. Farnsworth |
| sn               | Farnsworth |
| description      | Human |
| displayName      | Professor Farnsworth |
| employeeType     | Owner |
| employeeType     | Founder |
| givenName        | Hubert |
| jpegPhoto        | JPEG-Photo (630x507 Pixel, 26780 Bytes) |
| mail             | professor@globomantics.local |
| mail             | hubert@globomantics.local |
| ou               | Office Management |
| title            | Professor |
| uid              | professor |
| userPassword     | professor |


### cn=Philip J. Fry,ou=people,dc=globomantics,dc=local

| Attribute        | Value            |
| ---------------- | ---------------- |
| objectClass      | inetOrgPerson |
| cn               | Philip J. Fry |
| sn               | Fry |
| description      | Human |
| displayName      | Fry |
| employeeType     | Delivery boy |
| givenName        | Philip |
| jpegPhoto        | JPEG-Photo (429x350 Pixel, 22132 Bytes) |
| mail             | fry@globomantics.local |
| ou               | Delivering Crew |
| uid              | fry |
| userPassword     | fry |


### cn=John A. Zoidberg,ou=people,dc=globomantics,dc=local

| Attribute        | Value            |
| ---------------- | ---------------- |
| objectClass      | inetOrgPerson |
| cn               | John A. Zoidberg |
| sn               | Zoidberg |
| description      | Decapodian |
| displayName      | Zoidberg |
| employeeType     | Doctor |
| givenName        | John |
| jpegPhoto        | JPEG-Photo (343x280 Pixel, 26438 Bytes) |
| mail             | zoidberg@globomantics.local |
| ou               | Staff |
| title            | Ph. D. |
| uid              | zoidberg |
| userPassword     | zoidberg |

### cn=Hermes Conrad,ou=people,dc=globomantics,dc=local

| Attribute        | Value            |
| ---------------- | ---------------- |
| objectClass      | inetOrgPerson |
| cn               | Hermes Conrad |
| sn               | Conrad |
| description      | Human |
| employeeType     | Bureaucrat |
| employeeType     | Accountant |
| givenName        | Hermes |
| mail             | hermes@globomantics.local |
| ou               | Office Management |
| uid              | hermes |
| userPassword     | hermes |

### cn=Turanga Leela,ou=people,dc=globomantics,dc=local

| Attribute        | Value            |
| ---------------- | ---------------- |
| objectClass      | inetOrgPerson |
| cn               | Turanga Leela |
| sn               | Turanga |
| description      | Mutant |
| employeeType     | Captain |
| employeeType     | Pilot |
| givenName        | Leela |
| jpegPhoto        | JPEG-Photo (429x350 Pixel, 26526 Bytes) |
| mail             | leela@globomantics.local |
| ou               | Delivering Crew |
| uid              | leela |
| userPassword     | leela |

### cn=Bender Bending Rodriguez,ou=people,dc=globomantics,dc=local

| Attribute        | Value            |
| ---------------- | ---------------- |
| objectClass      | inetOrgPerson |
| cn               | Bender Bending Rodriguez |
| sn               | Rodriguez |
| description      | Robot |
| employeeType     | Ship's Robot |
| givenName        | Bender |
| jpegPhoto        | JPEG-Photo (436x570 Pixel, 26819 Bytes) |
| mail             | bender@globomantics.local |
| ou               | Delivering Crew |
| uid              | bender |
| userPassword     | bender |

### cn=Amy Wong+sn=Kroker,ou=people,dc=globomantics,dc=local

Amy has a multi-valued DN

| Attribute        | Value            |
| ---------------- | ---------------- |
| objectClass      | inetOrgPerson |
| cn               | Amy Wong |
| sn               | Kroker |
| description      | Human |
| givenName        | Amy |
| mail             | amy@globomantics.local |
| ou               | Intern |
| uid              | amy |
| userPassword     | amy |

### cn=admin_staff,ou=people,dc=globomantics,dc=local

| Attribute        | Value            |
| ---------------- | ---------------- |
| objectClass      | Group |
| cn               | admin_staff |
| member           | cn=Hubert J. Farnsworth,ou=people,dc=globomantics,dc=local |
| member           | cn=Hermes Conrad,ou=people,dc=globomantics,dc=local |

### cn=ship_crew,ou=people,dc=globomantics,dc=local

| Attribute        | Value            |
| ---------------- | ---------------- |
| objectClass      | Group |
| cn               | ship_crew |
| member           | cn=Turanga Leela,ou=people,dc=globomantics,dc=local |
| member           | cn=Philip J. Fry,ou=people,dc=globomantics,dc=local |
| member           | cn=Bender Bending Rodriguez,ou=people,dc=globomantics,dc=local |
