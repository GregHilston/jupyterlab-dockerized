# JuptyerLab Dockerized

A full blogpost is written on this repo on my personal site [here](http://greghilston.com/post/how-to-dockerize-jupyterlab/)

## How To Use

This repository provides an easy way to Dockerize a Jupyter Lab project. Annotate your dependencies in the `requirements.txt`, and then run `$ docker compose up`. The output of that command will emit a URL, with a token, which you can use to access the Jupyter Lab instance in your web browser. For example, it might look like:

```
jupyterlab-1  |     To access the server, open this file in a browser:
jupyterlab-1  |         file:///home/jovyan/.local/share/jupyter/runtime/jpserver-7-open.html
jupyterlab-1  |     Or copy and paste one of these URLs:
jupyterlab-1  |         http://c6bcfb18cb93:8888/lab?token=somefaketoken
jupyterlab-1  |         http://127.0.0.1:8888/lab?token=somefaketoken
```

Then you'd navigate to `http://127.0.0.1:8888/lab?token=somefaketoken` or `localhost:8888/lab?token=somefaketoken` in your web browser.

### Diclaimers

1. You'll notice that you have one directory labeled `work`. Please be aware that only the files you write into this directory will actually be saved, as this is the only directly that is volumed into the container by our `docker-compose.yaml` file.
2. If you want to install a new dependency, the easiest way is to modify the `requirements.txt` and restart the container. If that is to heavy handed, you can modify the `requirements.txt`, which will set you up for future exectuions, and then access a terminal inside the Jupyter Lab instance to install the dependency for this session.

## How Does This Work

We're relying on an existing Docker image called `jupyter/minimal-notebook`. This image has a [slew of common features documented here](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/common.html). We're taking advantage of the [Startup Hooks](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/common.html#startup-hooks), to ensure that your Python dependencies are automatically installed for us when we spin up a container.

## Selecting A Docker Image

I've decided to leverage [this image](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html#jupyter-minimal-notebook), but you can read through [this documentation](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html) to select your own. Be sure to change the `image` line in your `docker-compose.yaml` if you want to make a modification.

