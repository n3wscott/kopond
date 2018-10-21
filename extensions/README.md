# ko extensions 

I am attempting to add [extensions](https://github.com/google/go-containerregistry/pull/292) to ko to make some of my workloads easier.


Say, I have some code that I would like to be in the cloud: [echo](./cmd/echo/)

I use ko to push that as a Service from Knative:

```
⦿ ko service echo github.com/n3wscott/kopond/cmd/echo/
2018/10/21 11:26:21 Using base gcr.io/distroless/base:latest for github.com/n3wscott/kopond/cmd/echo/
2018/10/21 11:26:25 Publishing gcr.io/n3wscott/echo-f4a097be70ea2d0a78b8ee311b00ee08:latest
2018/10/21 11:26:26 mounted blob: sha256:e098b08362eaf731fcb51d353f00af11193eda59590598c1e78dc2fad4819db7
2018/10/21 11:26:26 mounted blob: sha256:655abe75b561e7cd0e8b1fc3375fe281f7ad7bbcd3060a5b5127c0b90a8aaf99
2018/10/21 11:26:26 mounted blob: sha256:28b63fe090157d2155af7b872bfa12510bc2a0f7f421ab0112a3b9056d692c8d
2018/10/21 11:26:26 mounted blob: sha256:07accba5256724c9927289c79e6e97675a949f42abef8b7321e133fe9713a8fe
2018/10/21 11:26:27 gcr.io/n3wscott/echo-f4a097be70ea2d0a78b8ee311b00ee08:latest: digest: sha256:610203348837f73887cad5b212d6517a2e03ac2ad2ddada2c1586505d29a6f88 size: 751
2018/10/21 11:26:27 Published gcr.io/n3wscott/echo-f4a097be70ea2d0a78b8ee311b00ee08@sha256:610203348837f73887cad5b212d6517a2e03ac2ad2ddada2c1586505d29a6f88
service.serving.knative.dev/echo created
```

It is running in k8s:

```
⦿ kubectl get ksvc echo
NAME      CREATED AT
echo      59s
```

And now I am done with it.

```
⦿ ko service delete echo
service.serving.knative.dev "echo" deleted
[11:28:18] nicholss@nicholss-1 ~/go/src/github.com/google/go-containerregistry (move-cmd)
```

It is gone from k8s:

```
⦿ kubectl get ksvc echo
No resources found.
Error from server (NotFound): services.serving.knative.dev "echo" not found
```

---

To enable this, patch [#292](https://github.com/google/go-containerregistry/pull/292) and add the ./bin files to your path.