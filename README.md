# Certificate SSl in localhost

The purpose of this repository is to create an ssl certified development environment (localhost)
secure with using docker.

The `steps to generate a certificate` will be shown as an example to generate
the certificate and the creation of web services (apache2) and another reverse proxy (traefik).

Within the file traefik.yml you can find the service settings.

NOTE: In the file traefik.yml, a local network was created with a fixed ip for each container, but this is optional.

## Dependencies

- Operational system Ubuntu
- git
- libnss3-tools
- Homebrew
- mkcert

### Install

```
sudo apt install git

sudo apt install libnss3-tools

git clone https://github.com/Homebrew/brew ~/.linuxbrew/Homebrew
mkdir ~/.linuxbrew/bin
ln -s ~/.linuxbrew/Homebrew/bin/brew ~/.linuxbrew/bin
eval $(~/.linuxbrew/bin/brew shellenv)

brew install mkcert
```

If your system operating is differently, please see [mkcert](https://github.com/FiloSottile/mkcert)

### Clone repository

```
git clone https://github.com/rutepassos/traefik-ssl

```

### Steps for create services with routing traefik

```
cd traefik-ssl

mkcert -cert-file certs/local-traefik-cert.pem -key-file certs/local-traefik-key.pem  "php5.localhost" "*.php5.localhost" "php7.localhost" "*.php7.localhost"

docker-compose -f traefik.yml up -d

```

### Steps for create services without traefik

```

cd traefik-ssl

mkcert -cert-file certs/local-cert.pem -key-file certs/local-key.pem  "localhost" "*.localhost"

docker-compose up -d

```

You can now go to your browser at [https://php5.localhost](https://php5.localhost) and [https://php7.localhost](https://php7.localhost), enjoy!!!.

You can now go to your browser the traefik dashboard [http://localhost:8080/dashboard](http://localhost:8080/dashboard).

Inspired by:

- [https://docs.docker.com/](https://docs.docker.com/)
- [https://docs.traefik.io/](https://docs.traefik.io/)
- [https://github.com/Heziode/traefik-v2-https-ssl-localhost](https://github.com/Heziode/traefik-v2-https-ssl-localhost)
- [https://github.com/FiloSottile/mkcert](https://github.com/FiloSottile/mkcert)
