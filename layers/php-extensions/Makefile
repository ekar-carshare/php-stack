extensions := ddtrace fpm-prometheus xdebug

.DEFAULT_GOAL := build
.PHONY: build publish $(extensions)

publish build: $(extensions)

$(extensions):
	$(MAKE) $(MAKECMDGOALS) IMAGE_TAG=$(IMAGE_TAG) -C "$@"
