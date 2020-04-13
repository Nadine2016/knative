---

copyright:
  years: 2020
lastupdated: "2020-04-13"

keywords: knative

subcollection: knative

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}

# Building a container image from your source code
{: #kn-job-build}

Learn how to build a container image from your source code. 
{: shortdesc}

    - Where should I store the code
    - What needs to be included in my image? 
    - Best practices for creating the image to support common user scenarios.
    - How do I migrate common non-containerized jobs? 
    - Where should I store the image?

1. Fork the repo [jeremiaswerner/knative_demo](https://github.com/jeremiaswerner/knative_demo){: external} 

   * open the page and click on fork in the upper right corner of the repo
   * specify the target repository, typically your GitHub account
   * Press on "Clone or download" and copy the "ssh" url
   * Checkout the git repository with `git clone git@github.com:jeremiaswerner/knative_demo.git`
   
2. Register and Login to [DockerHub](https://hub.docker.com/){: external}

In the demo below you can exchange the image repository `jeremiaswerner/helloworld` with your personal repository and image.

3. In the folder where you checked out your repository, you can view and modify the Dockerfile:

   ```
   $ cat Dockerfile
   FROM golang:alpine
   COPY helloworld.go /
   RUN go build -o /helloworld /helloworld.go
   ENTRYPOINT [ "/helloworld" ]
   ```

4. Build the image and push it to your docker registry

   ```
   docker build . && docker push <your-docker-repo>/helloworld 
   ```

5. Use this uploaded image to create your custom Knative service as described in steps 4-5

More sophisticated examples can be found in the Knative community, see [sample](https://github.com/knative/docs/tree/master/docs/serving/samples){: external}
