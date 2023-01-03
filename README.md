# DevOps Task

Our homework assignment is designed to let you show off your skill in two areas of expertise: software development and systems administration. To successfully complete the homework and make a good impression you'll need to draw upon both disciplines.
Your goal is to provide a working image colorization service. This service will accept JSON requests of this form:

```    
    {
      "op": "blueify",
      "image": "iVBORw...SuQmCC"
    }
```

Where:
* `"op"` is a colorization operation: `"blueify"`, `"greenify"`, or `"reddify"`, and
* `"image"` is the base64-encoded image to be colorized

It will return JSON of this form:
```    
    {
      "ip": "192.158.1.38",
      "created": "1666300434",
      "image": "/9j/4AAQ...ooA//Z"
    }
```
Where:

* `"ip"` is the IP address of the Kubernetes pod that did the work
* `"created"` is the boot time of the pod, and
* `"image"` is the base64-encoded image colorized as requested

We ask that you provide this service via a publicly-accessible Kubernetes cluster with a minimum of 3 running nodes. The Homework Submission Server will send several colorization requests to your cluster and will look for at least 3 different IP addresses to be sent back in the reply packets (along with the properly encoded images).
The hard part of this task has been done for you. We're supplying the colorization server in the form of a binary executable. This server:

* listens for TCP connections on port 8080
* accepts image colorization requests
* formats images according to the requested operation
* calls the Kubernetes API to obtain the pod's IP address and boot time
* returns the image, IP, and boot time to the requester

However, this server has a couple quirks. It:

* only runs on ARM-based Linux Kubernetes pods, and
* communicates using Protobuf instead of JSON

The server may require a cluster role binding to provide it with the proper permissions. This can be done with a command similar to this:

```
kubectl create clusterrolebinding default-view --clusterrole=view --serviceaccount=default:default
```

These quirks are there to give you the opportunity to show off your coding skills. You'll need to design and implement a transcoding layer that will take JSON requests from the Homework Submission Server and transform them into gRPC calls to the Colorization Server.

It's up to you to decide how to complete the task. We are asking that these requirements be met:

* Use the server binary that we supply to do the image manipulation
* Set up the binary as a Kubernetes service running on at least three different pods on separate nodes
* Make your service accessible to the Homework Submission Server
* Write unit tests exercising the essential functionality of your code

After you have succesfully made a submission you may shut down the Kubernetes cluster and any other active resources you set up. The submission server records successful submissions so it is not necessary to maintain an active cluster.

**This task should take an appropriately trained mid-level developer with devops experience around 4 hours to complete.**

### Submission

* URL of running kubernetes cluseter
* Image colorization service
