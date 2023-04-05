
BASIC_IMG = buggy-basic
SCRATCH_IMG = buggy-scratch
DELVE_IMG = buggy-delve

.PHONY: bin/dlv
bin/dlv:
	go build -o ../bin/dlv
.PHONY: build-image
build-image: 
	docker build --rm -f build/Dockerfile -t $(BASIC_IMG):latest .
 
.PHONY: run-basic-image
run-basic-image: 
	docker run -it --detach -p 8080:8080 --rm $(BASIC_IMG)

.PHONY: curl-app
curl-app: 	
	curl localhost:8080/foo/bar
.PHONY: copy-dlv-to-container
copy-dlv-to-container:
	$(info "Container Id is:" $(shell docker ps -aqf "ancestor=$(BASIC_IMG)"))
	docker cp ../bin/dlv $(shell docker ps -aqf "ancestor=$(BASIC_IMG)"):/dlv

.PHONY: exec-dlv-basic-container
exec-dlv-basic-container:
	docker exec -it $(shell docker ps -aqf "ancestor=$(BASIC_IMG)") dlv attach 1

.PHONY: run-basic-image-with-ptrace
run-basic-image-with-ptrace: 
	docker run -it --detach --rm -p 8080:8080 --privileged --cap-add=SYS_PTRACE $(BASIC_IMG)

.PHONY: exec-dlv-container-with-src 
exec-dlv-container-with-src:
	docker cp ./ $(shell docker ps -aqf "ancestor=$(BASIC_IMG)"):/src
	docker cp D:/Go $(shell docker ps -aqf "ancestor=$(BASIC_IMG)"):/goroot
	docker exec -it $(shell docker ps -aqf "ancestor=$(BASIC_IMG)") dlv --init=/src/hack/delve-container-initfile attach 1
