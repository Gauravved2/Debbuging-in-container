To debug a binary in the container the approach that we have followed is of copying the delve(dlv) file produced by the go build command.
First we build the docker image and execute it using make build-image
make bin/dlv is used to create the dlv file created by go build.
make run-basic-image is used to run the command.
make curl-app is used to make sure that app is working
make copy-dlv-to-container is used to copy the dlv to the container. 
    Here the command used is  docker cp ../bin/dlv $(shell docker ps -aqf "ancestor=$(BASIC_IMG)"):/dlv for windows.
    In windows to execture another shell (in this case docker) command within another command from the make file we use shell.
    For Linux or mac this command be different :- docker cp ../bin/dlv $$(docker ps -aqf "ancestor=$(BASIC_IMG)"):/dlv like removing shell adding $$ instead of $
