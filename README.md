# Custom Default Backend for NGINX Ingress Controller

<p align="center">
  <a href="https://hub.docker.com/repository/docker/nitrocode/pipeops-custom-backend" alt="Docker Version">
    <img src="https://img.shields.io/docker/v/nitrocode/pipeops-custom-backend?label=version&sort=semver"/>
  </a>
  <a href="https://hub.docker.com/repository/docker/nitrocode/pipeops-custom-backend" alt="Docker Pulls">
    <img src="https://img.shields.io/docker/pulls/nitrocode/pipeops-custom-backend"/>
  </a>
  <a href="https://hub.docker.com/repository/docker/nitrocode/pipeops-custom-backend" alt="Docker Image size">
    <img src="https://img.shields.io/docker/image-size/nitrocode/pipeops-custom-backend?sort=date"/>
  </a>
  <a href="LICENSE" alt="GitHub License">
    <img src="https://img.shields.io/github/license/nitrocode/pipeops-custom-backend?label=license"/>
  </a>
</p>

Customize the default backend for an NGINX Ingress Controller on your kubernetes cluster. A single Docker image with an NGINX server that handles most status codes.

[LIVE Preview - 404 status code](https://billowy-in2-pipeops-3d5d08ea.pipeops.app)

[LIVE Preview - 503 status code](https://filthy-sign-pipeops-981f3e30.pipeops.app)

## Installation via Helm
You can use the `defaultBackend` property of the [ingress-nginx](https://github.com/kubernetes/ingress-nginx/tree/main/charts/ingress-nginx) helm chart like this:

```
defaultBackend:
  enabled: true
  image:
    # Or your own forked one...
    repository: nitrocode/pipeops-custom-backend
    tag: "latest"
    pullPolicy: Always
  port: 8080
```

## HTML Customization

Fork this repository and edit the HTML inside the `content/` directory if you want some CSS / text customization.

If you wish to have a different HTML error page per status code you can omit the `ssi` part and set up the error pages (e.g. `content/404.html`, `content/500.html`) like this:

```
# default.conf
server {
  # ...
  error_page 400 /404.html;
  location = /404.html {
    internal;
  }
  error_page 500 /500.html;
  location = /500.html {
    internal;
  }
  # ...
}
```
