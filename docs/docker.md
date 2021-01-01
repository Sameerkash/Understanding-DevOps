## Understanding Docker

**Contents**

- [Some Theory](#some-theory)

### Some theory

So what exactly is docker? Well, that's a question with multiple answers.

But first, what do you mean by "What is docker?", to that, the answer will be,

`Docker` is a platform, consisting of several tools :-

###### Docker Engine

is a client-server application, it consists of a server called `docker daemon` a REST API service and the CLI. The Client is the way users interact with the docker daemon and tell the server what to do, for example. The daemon listens for Docker API requests and manages Docker objects such as images, containers, networks

```pseudocode
docker pull mongo
```

This command tells docker to pull down an image from a registry.

###### Registries

_Registries_ are to containers, what _GitHub_ is to code. Meaning, it is a public/private repository where you can store your images.

###### Images

Images are a snapshot of the filesystem of your project, it is essentially an immutable copy which is packed as a single object

###### Containers

Containers are an instance of an image, it is a image in execution just like any other program but, the difference being, containers are isolated, having their own space, network, and resources separate from anything else running on the machine.
