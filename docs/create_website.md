# Create website

Used a Jeff Geerling tutorial to run though this:
- https://www.jeffgeerling.com/blog/2022/quick-hello-world-http-deployment-testing-k3s-and-traefik

Supplemented by another tutorial that acutally used the container build 
process. This is more likely what I would do since my projects would have use
a more intense backend.
- https://medium.com/@samanazizi/how-to-deploy-a-simple-static-html-project-on-k3s-322667967ed4

## Create (a super simple) website

Build a simple website. In the tutorials case, it was just a single html file.
Put this website it its own directory. Even if it is as simple as an index.html
file inside a folder.

## Create a Containerfile

To create a container, build the docker container. Keep in mind that the final
image is not stored in a file by default. It is instead created and stored in
docker/podman memory somewhere. Knowing how/where might be nice, but it is 
unimportant for the time being.

This particular Containerfile is quite simple. It uses a parent container 
based on the dockerhub nginx container and then copies over the index.html we
created.

Once the Containerfile has been built, it is ready to be used. To test a non-
kubernetes deployment of the container, you could run it in a normal container
environment. It should be able to be exported and imported to other nodes if
necessary.

## Apply the manifest

The configuration yml file is called a manifest. It is what determines all the
various parameters that kubernetes needs to know. Most of the actuall app is
managed by the container itself.

The pods will then spin up as requested in the manifest. In particular, the
identified number of replicates to create is what determines how many pods are
created and kept running. If this is set to 0 (zero), no pods are created.

## Next steps?

For now, not much else to do here for me. We could make the hello-world website
much more interesting, but I've already built many websites and would rather 
not start from scratch.

As an alternative, I would like to start a new project and move over some 
websites that I've already created.
