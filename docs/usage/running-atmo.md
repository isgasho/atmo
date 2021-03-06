# Running Atmo

{% hint style="warning" %}
Atmo is still in Alpha, and as such should not yet be used for production workloads.
{% endhint %}

Atmo is distributed as a Docker image: `suborbital/atmo` 

To run Atmo, you can either mount your Runnable Bundle as a volume, or build your own container image that embeds it.

### Volume mount

To mount as a volume:

```text
> docker run -v /path/to/bundle/directory:/home/atmo -e ATMO_HTTP_PORT=%s -p 8080:8080 suborbital/atmo:latest atmo
```

This will launch Atmo, assign it to listen on port 8080, and run in HTTP mode.

### Embed Bundle

To create your own Docker image with your Bundle embedded, you can use a Dockerfile similar to this:

```yaml
FROM suborbital/atmo:latest

COPY ./runnables.wasm.zip .

ENTRYPOINT atmo
```

Building this Dockerfile would result in an image that doesn't need a volume mount.

#### HTTPS

To run with HTTPS, replace `ATMO_HTTP_PORT`with `ATMO_DOMAIN` to enable LetsEncrypt on ports 443 and 8080.

