# Use:
#
# `make container` will build a container
# `make save` will save the container as a tar ball

IMAGE_NAME ?=faiss
DOCKER_FILE ?=Dockerfile
JUPYTER_IMAGE_NAME ?=faiss-jupyter
JUPYTER_DOCKER_FILE ?=Dockerfile.jupyter
JUPYTER_PORT ?=8080

file := 'VERSION'
VERSION := $(shell cat ${file})

container:
	docker build --pull -t $(IMAGE_NAME) -f ${DOCKER_FILE} .
	docker tag $(IMAGE_NAME) $(IMAGE_NAME):$(VERSION)

save: container
	docker save -o $(IMAGE_NAME).tar $(IMAGE_NAME)

jupyter: container
	docker build --build-arg FAISS_VERSION=$(VERSION) -t $(JUPYTER_IMAGE_NAME) -f ${JUPYTER_DOCKER_FILE} .
	docker tag $(JUPYTER_IMAGE_NAME) $(JUPYTER_IMAGE_NAME):$(VERSION)

run_notebooks: jupyter
	docker run --rm -p $(JUPYTER_PORT):8888 -v $(NOTEBOOKS_DIR):/notebooks $(JUPYTER_IMAGE_NAME):$(VERSION) jupyter notebook --notebook-dir=/notebooks --ip 0.0.0.0 --no-browser --allow-root
