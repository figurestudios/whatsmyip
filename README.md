# whatsmyip
Simple Golem task that uses internet access to retrieve the provider's IP address.

Uses [golem_cuda](https://github.com/norbibi/golem_cuda) for internet connectivity.

## Running

### Prerequisites:
 - Go through the [quick primer example](https://handbook.golem.network/requestor-tutorials/flash-tutorial-of-requestor-development) followed by [run first task on Golem](https://handbook.golem.network/requestor-tutorials/flash-tutorial-of-requestor-development/run-first-task-on-golem) to get your environment setup.
 - Note that you do not need any additional dependencies to run internet-enabled applications, you only need them to create them from scratch using Buildroot.
 - Clone this repository and `cd` into it with your Yagna daemon running with your environment enabled and configured.
 - Run `python3 requestor.py` and wait for a result like this:
 ```
[2022-08-09T16:05:28.684+0200 INFO yapapi.summary] [Job 1] Agreement proposed to provider 'm4'
[2022-08-09T16:05:29.053+0200 INFO yapapi.summary] [Job 1] Agreement confirmed by provider 'm4'
[2022-08-09T16:05:30.368+0200 INFO yapapi.summary] Received proposals from 1 provider so far
[2022-08-09T16:05:35.983+0200 INFO yapapi.summary] [Job 1] Task started on provider 'm4', task data: None
78.197.xxx.xx
[2022-08-09T16:05:49.485+0200 INFO yapapi.summary] [Job 1] Task finished by provider 'm4', task data: None
[2022-08-09T16:05:50.488+0200 INFO yapapi.executor] [Job 1] Waiting for 1 worker to finish...
[2022-08-09T16:05:51.201+0200 INFO yapapi.executor] [Job 1] Waiting for Executor services to finish...
[2022-08-09T16:05:51.203+0200 INFO yapapi.executor] Golem is shutting down...
[2022-08-09T16:05:51.206+0200 INFO yapapi.summary] [Job 1] Job finished in 117.0s
[2022-08-09T16:05:51.209+0200 INFO yapapi.summary] [Job 1] Negotiated 1 agreements with 1 provider
[2022-08-09T16:05:51.212+0200 INFO yapapi.summary] [Job 1] Provider 'm4' computed 1 task
[2022-08-09T16:05:51.214+0200 INFO yapapi.executor] All jobs have finished
[2022-08-09T16:05:51.215+0200 INFO yapapi.executor] 1 agreement still unpaid, waiting for invoices...
[2022-08-09T16:05:51.805+0200 INFO yapapi.summary] [Job 1] Accepted invoice from 'm4', amount: 0.005586913921944444
[2022-08-09T16:05:51.806+0200 INFO yapapi.executor] Waiting for Golem services to finish...
[2022-08-09T16:05:51.834+0200 INFO yapapi.summary] Total cost: 0.005586913921944444
[2022-08-09T16:05:51.835+0200 INFO yapapi.summary] Golem engine has shut down
 ```

## Explanation

By looking for certain [capabilities](https://github.com/figurestudios/whatsmyip/blob/issue1/requestor.py#L30), we can look for attributes that work on providers even if they are not included in the official provider software. Thanks to [golem_cuda](https://github.com/norbibi/golem_cuda), we now have CUDA in the Yagna VM runtime on a few providers. With this fork, we also got limited internet access. Using [an example](https://github.com/norbibi/yapapi/blob/24881c9d1ecf80be7ad6b8d56f3f72a71403f64a/examples/ffmpeg_cuda/docker_golem_ffmpeg_cuda/Dockerfile) as a base, I was able to [upload](https://github.com/figurestudios/whatsmyip/blob/main/requestor.py#L15) and [run](https://github.com/figurestudios/whatsmyip/blob/main/requestor.py#L16) my own code to make use of the internet access and with it, this repository was created. Feel free to use this as an example until we have more general-use images created, as building your own with Buildroot is more advanced than you'd think. The author of [golem_cuda](https://github.com/norbibi/golem_cuda) is experimenting with building Docker images using apt over Buildroot, which might make it easier in the future.
