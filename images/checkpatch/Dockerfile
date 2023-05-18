# syntax=docker/dockerfile:1.1-experimental
# SPDX-License-Identifier: Apache-2.0
# Copyright 2020 Authors of Cilium

ARG ALPINE_BASE_IMAGE=docker.io/arm64v8/alpine:3.16.5@sha256:de0254f3bb409dcf0c3750950afa18cfbcf763372cfbecd1161a095c76438f09

FROM ${ALPINE_BASE_IMAGE} as builder
LABEL maintainer="maintainer@cilium.io"

COPY . /checkpatch

RUN apk add --no-cache bash curl git jq moreutils patch perl

RUN for i in /checkpatch/fixes/*.diff; do \
    patch -p1 /checkpatch/checkpatch.pl < "$i"; \
    done

ENTRYPOINT ["/checkpatch/checkpatch.sh"]
