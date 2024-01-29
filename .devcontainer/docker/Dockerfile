## Base on Python dev container
FROM registry.remote.sx/development-images/ubuntu/python:latest

## Install mkdocs-material theme and plugins
RUN python3 -m pip install --break-system-packages \
        mkdocs-material \
    && python3 -m pip install --break-system-packages \
        mkdocs-git-revision-date-localized-plugin \
        mkdocs-glightbox

## Set the work directory
WORKDIR /code