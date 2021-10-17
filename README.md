# parsedmarc-dockerized

Note: The standalone `parsedmarc` docker image on [DockerHub @ sunred/parsedmarc](https://hub.docker.com/r/sunred/parsedmarc) can also be used, if interested.

## Setup:
1. Get basics together:
```
git clone https://git.snrd.de/sunred/parsedmarc-dockerized.git /opt/parsedmarc-dockerized/
cd /opt/parsedmarc-dockerized/ && cp data/conf/parsedmarc/config.sample.ini data/conf/parsedmarc/config.ini
```

2. Next we change the `parsedmarc` config (see [docs](https://domainaware.github.io/parsedmarc/#configuration-file). You can set `Test` to `True` for testing purposes.)
```
nano data/conf/parsedmarc/config.ini
```

3. To use the geoip updater for automatic geo location resolution you have to [create an account](https://www.maxmind.com/en/geolite2/signup) on the MaxMind website and add your license key you can retrieve from your [account page](https://www.maxmind.com/en/account) to `data/conf/geoipupdate.env`. More information in the [documentation](https://crazymax.dev/geoip-updater/usage/prerequisites/).

4. Finally, we start up the stack and wait:
```
docker-compose up -d
```

### What's happening then?

1. First, containers of the stack are created and started. This might take a while, as several containers have dependencies on others being in a healthy state (meaning that its service must be fully started).
2. During the startup of the `parsedmarc-init` container, all required steps and preparations are being taken care of - like generating a self-signed certificate for the included `nginx` webserver.
3. Once the Kibana container - where you can view the dashboards - is started up, the corresponding parsedmarc dashboards are automatically imported into Kibana by the `parsedmarc-init` container.
4. After a while, when everything is up and running, you can then access Kibana and its dashboards at `localhost:5601` that you can reverse proxy on your host system.

## Credits

Built with awesome [parsedmarc](https://github.com/domainaware/checkdmarc), [Elasticsearch and Kibana](https://www.elastic.co/), [Docker](https://docker.com) and [MaxMind GeoIP](https://dev.maxmind.com/geoip/geoip2/geolite2/).
