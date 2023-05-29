# Traefik via docker


```toml
# generated 2023-04-21, Mozilla Guideline v5.6, Traefik 2.1.2, modern configuration
# https://ssl-config.mozilla.org/#server=traefik&version=2.1.2&config=modern&guideline=5.6
[http.routers]
  [http.routers.router-secure]
    rule = "Host(`example.com`)"
    service = "service-id"
    middlewares = ["hsts-header"]

    [http.routers.router-secure.tls]
      options = "modern"

  [http.routers.router-insecure]
    rule = "Host(`example.com`)"
    service = "service-id"
    middlewares = ["redirect-to-https", "hsts-header"]

[http.middlewares]
  [http.middlewares.redirect-to-https.redirectScheme]
    scheme = "https"
  [http.middlewares.hsts-header.headers]
    [http.middlewares.hsts-header.headers.customResponseHeaders]
      Strict-Transport-Security = "max-age=63072000"

# due to Go limitations, it is highly recommended that you use an ECDSA
# certificate, or you may experience compatibility issues
[[tls.certificates]]
  certFile = "/path/to/signed_cert_plus_intermediates"
  keyFile = "/path/to/private_key"

[tls.options]
  [tls.options.modern]
    minVersion = "VersionTLS13"
```
https://ssl-config.mozilla.org/#server=traefik&version=2.9.10&config=modern&guideline=5.6
