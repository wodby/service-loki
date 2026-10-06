# Grafana Loki on Wodby

What Wodby sets up for Loki on this service. It runs from the official `grafana/loki` image as a single instance with the configuration file shipped in the image, `/etc/loki/local-config.yaml`.

- Loki listens on port 3100, which is private. Other services in the environment reach it at `http://<Loki service name>:3100`; Grafana uses that address as the data source URL.
- With the image's configuration, authentication is off (`auth_enabled: false`) and chunks, index and rules are stored on the local filesystem under `/loki`.
- The `data` volume is mounted at `/loki`, so that data is persistent.
- The manifest has no settings, links, config files, backups or actions. The configuration file is part of the image and is not on a volume: do not edit it in the container.
- `/ready` on port 3100 answers when Loki can accept requests.
