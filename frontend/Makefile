IMAGE_NAME = f2-reviewrot-frontend

build:
	docker build -t $(IMAGE_NAME) .

deploy:
	oc start-build $(IMAGE_NAME)

destroy:
	oc delete {bc,dc,is}/$(IMAGE_NAME)

create:
	oc new-app https://github.com/ralphbean/f2-reviewrot-openshift \
		--context-dir=frontend \
		--strategy=docker \
		--name $(IMAGE_NAME)
	oc volume dc/$(IMAGE_NAME) --add \
		--name=json-data \
		--mount-path=/opt/data
