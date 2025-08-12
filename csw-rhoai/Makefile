IMAGE      ?= csw-odh
DATE_TAG   ?= $(shell date +%Y-%m-%d)
PORT       ?= 8888

RUN_TAG    := run-$(DATE_TAG)
DEV_TAG    := dev-$(DATE_TAG)

#CHANGE BASED ON REPO
IMAGE_REPO ?= quay.io/memalhot/cuda

.PHONY: build-run build-dev run-run run-dev

build-run:
	@echo "Building $(IMAGE):$(RUN_TAG) from Containerfile.run"
	podman build -t $(IMAGE):$(RUN_TAG) -f Containerfile.run .

pub-run: build-run
	podman push $(IMAGE):$(RUN_TAG) $(IMAGE_REPO):run-$(RUN_TAG)

build-dev:
	@echo "Building $(IMAGE):$(DEV_TAG) from Containerfile.dev"
	podman build -t $(IMAGE):$(DEV_TAG) -f Containerfile.dev .

pub-run: build-run
	podman push $(IMAGE):$(RUN_TAG) $(IMAGE_REPO):run-$(RUN_TAG)

run-run: build-run
	@echo "Running $(IMAGE):$(RUN_TAG) on http://localhost:$(PORT)"
	podman run -it --rm \
		-p $(PORT):$(PORT) \
		$(IMAGE):$(RUN_TAG)

run-dev: build-dev
	@echo "Running $(IMAGE):$(DEV_TAG) on http://localhost:$(PORT)"
	podman run -it --rm \
		-p $(PORT):$(PORT) \
		$(IMAGE):$(DEV_TAG)
