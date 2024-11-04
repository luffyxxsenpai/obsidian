# dockerfile
---
Date: 13,Oct,2024
subject:  all about dockerfile
field: [[docker]] [[devops]]
tags: #dockerfile

---

# DOCKERFILE

- DOCKERFILE should be named Dockerfile
- its all about INSTRUCTION argument
- its advised to write INSTRUCTIONS in caps to differentiate it from arguments\


### example
```bash
# INSTRUCTIONS arguments

# FROM is to define the base image FROM imagename:version
FROM  alpine:3.18

# LABEL to lable the image
LABEL name="luffy"
LABEL email="luffy@gmail.com"

# argument is passed white building the image 
ARG key=value
 


# RUN is to executes command during image building
# RUN works in 2 format  SHELL and EXEC format
# SHELL - we dont have to define which shell we using
# EXEC - we define which shell
RUN apk add curl

# WORKDIR we can set the working directory
# by default images use / 
# if that directory is not present it will create it so nothing to worry
WORKDIR /myapp

# by default docker uses root to run commands we can create our own users to exec
RUN adduser -D luffy
USER luffy

# ENV variables can be defined by ENV key=value
ENV app_host='0.0.0.0'
ENV app_port=5000\
    abc=xyz\
    mno=pqr

# COPY helps us copying something from source to destination
# COPY SOURCE DESTINATION
COPY abc.txt /myapp

# ADD can do it too but it can also do remote files like s3objects 
# ADD can also automatically extract any tar files and all in destination
ADD https://mybucket.s3.amaoznaws.com/abc.txt /myapp


# EXPOSE to expose ports 
# expose doesnt open ports manually its like a documentation
EXPOSE 5000


# CMD to execute commands
# everypart of command in its own quote
CMD ["a", "b", "c"]


# ENTRYPOINT
ENTRYPOINT ["a","b","c"]

# difference between entrypoint and cmd is that 
# entrypoint acts like a prefix , will be present before every command
# we cant change entryproint manually



```


`docker build -t imagename:version .`
`docker build -t imagename:version -f /path/to/dockerfile`

