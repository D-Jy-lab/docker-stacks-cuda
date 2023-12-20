# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.

# https://hub.docker.com/r/jupyter/base-notebook/tags
ARG OWNER=duan2001
ARG BASE_CONTAINER=$REGISTRY/$OWNER/base-notebook:2023-11-17
FROM $BASE_CONTAINER

LABEL maintainer="Jupyter Project <jupyter@googlegroups.com>"

# Fix: https://github.com/hadolint/hadolint/wiki/DL4006
# Fix: https://github.com/koalaman/shellcheck/wiki/SC3014
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ENV TAG="2023-11-17"

COPY --chown=${NB_UID}:${NB_GID} binder/README.ipynb "${HOME}"/README.ipynb
