.DEFAULT_GOAL := build
.PHONY: build publish

export DOCKER_BUILDKIT ?= 1
export IMAGE_REGISTRY := docker.io
export IMAGE_USER := gbmcarlos
export IMAGE_REPO := php-base
export IMAGE_TAG := latest
export ARCHES := arm64 amd64
export IMAGE_NAME := ${IMAGE_REGISTRY}/${IMAGE_USER}/${IMAGE_REPO}:${IMAGE_TAG}

build:
	for arch in ${ARCHES}; do \
		docker build \
		--platform linux/$$arch \
		-t ${IMAGE_NAME}-$$arch \
		--target base \
		--build-arg COMPOSER_VERSION \
		--build-arg PHP_VERSION \
		${CURDIR} ; \
	done

publish: build
	docker manifest rm ${IMAGE_NAME}
	for arch in ${ARCHES}; do \
  		docker push ${IMAGE_NAME}-$$arch ; \
  		docker manifest create ${IMAGE_NAME} --amend ${IMAGE_NAME}-$$arch ; \
	done
	docker manifest push ${IMAGE_NAME}
