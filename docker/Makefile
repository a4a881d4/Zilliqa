
.PHONY: all ci k8s-zilliqa k8s-scilla

# build the default zilliqa docker image same as the one on Docker Hub
all:
	docker build -t zilliqa .

# build zilliqa docker image for CI usage
ci:
	docker build -t zilliqa-ci -f Dockerfile.ci .


len=$(shell echo $(COMMIT) | wc -c)
commit=$(shell echo $(COMMIT) | cut -c 1-7)

check-commit:
	@if [ -z "$(COMMIT)" ]; \
	then \
		echo "COMMIT=xxxxxxx is not passed in after make target"; \
		exit 1; \
	fi
	@if [ $(len) -lt 7 ]; \
	then \
		echo "COMMIT doesn't have enough length (at least 7)"; \
		exit 1; \
	fi

# build zilliqa docker image for Kubernetes usage
k8s-zilliqa: check-commit
	cat Dockerfile Dockerfile.k8s | docker build -t zilliqa:$(commit) \
		--build-arg COMMIT=$(commit) -

k8s-scilla: check-commit
	cat Dockerfile Dockerfile.k8s | docker build -t zilliqa:$(commit).scilla \
		--build-arg COMMIT=$(commit) --build-arg BASE=zilliqa/scilla -

