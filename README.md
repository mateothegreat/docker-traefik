# Traefik via docker

```bash
docker compose up
```

You should see output like the following:

```bash
traefik         | time="2023-05-29T17:52:02Z" level=debug msg="Adding route for sandbox.matthewdavis.io with TLS options default" entryPointName=web
traefik         | time="2023-05-29T17:52:02Z" level=debug msg="Looking for provided certificate(s) to validate [\"sandbox.matthewdavis.io\"]..." ACME CA="https://acme-v02.api.letsencrypt.org/directory" providerName=myresolver.acme
traefik         | time="2023-05-29T17:52:02Z" level=debug msg="Domains [\"sandbox.matthewdavis.io\"] need ACME certificates generation for domains \"sandbox.matthewdavis.io\"." ACME CA="https://acme-v02.api.letsencrypt.org/directory" providerName=myresolver.acme
traefik         | time="2023-05-29T17:52:02Z" level=debug msg="Loading ACME certificates [sandbox.matthewdavis.io]..." providerName=myresolver.acme ACME CA="https://acme-v02.api.letsencrypt.org/directory"
traefik         | time="2023-05-29T17:52:03Z" level=debug msg="Building ACME client..." providerName=myresolver.acme
traefik         | time="2023-05-29T17:52:03Z" level=debug msg="https://acme-v02.api.letsencrypt.org/directory" providerName=myresolver.acme
traefik         | time="2023-05-29T17:52:03Z" level=info msg=Register... providerName=myresolver.acme
traefik         | time="2023-05-29T17:52:03Z" level=debug msg="legolog: [INFO] acme: Registering account for matthew@matthewdavis.io"
traefik         | time="2023-05-29T17:52:03Z" level=debug msg="Using TLS Challenge provider." providerName=myresolver.acme
traefik         | time="2023-05-29T17:52:03Z" level=debug msg="legolog: [INFO] [sandbox.matthewdavis.io] acme: Obtaining bundled SAN certificate"
traefik         | time="2023-05-29T17:52:04Z" level=debug msg="legolog: [INFO] [sandbox.matthewdavis.io] AuthURL: https://acme-v02.api.letsencrypt.org/acme/authz-v3/232176922377"
traefik         | time="2023-05-29T17:52:04Z" level=debug msg="legolog: [INFO] [sandbox.matthewdavis.io] acme: use tls-alpn-01 solver"
traefik         | time="2023-05-29T17:52:04Z" level=debug msg="legolog: [INFO] [sandbox.matthewdavis.io] acme: Trying to solve TLS-ALPN-01"
traefik         | time="2023-05-29T17:52:04Z" level=debug msg="TLS Challenge Present temp certificate for sandbox.matthewdavis.io" providerName=tlsalpn.acme
traefik         | time="2023-05-29T17:52:04Z" level=debug msg="Configuration received: {\"http\":{},\"tcp\":{},\"udp\":{},\"tls\":{}}" providerName=tlsalpn.acme
traefik         | time="2023-05-29T17:52:04Z" level=debug msg="Adding certificate for domain(s) acme challenge temp,sandbox.matthewdavis.io"raefik via docker
traefik         | time="2023-05-29T17:49:10Z" level=error msg="The ACME resolver \"myresolver\" is skipped from the resolvers list because: unable to get ACME account: read /acme.json: is a directory"
```

Test and verify the SSL certificate is applied correctly:

```bash
curl -v https://sandbox.matthewdavis.io
```

```bash
* Server certificate:
*  subject: CN=sandbox.matthewdavis.io
*  start date: May 29 16:52:11 2023 GMT
*  expire date: Aug 27 16:52:10 2023 GMT
*  subjectAltName: host "sandbox.matthewdavis.io" matched cert's "sandbox.matthewdavis.io"
*  issuer: C=US; O=Let's Encrypt; CN=R3   <----------- here
*  SSL certificate verify ok.             <----------- here
```

# See also

* https://ssl-config.mozilla.org/#server=traefik&version=2.9.10&config=modern&guideline=5.6
