# triton-notes

## Run Triton Server
```bash
docker run --gpus all --rm --shm-size=1g --ipc=host --ulimit memlock=-1 --ulimit stack=67108864 -p8000:8000 -p8001:8001 -p8002:8002 -v <your-models-dir>:/models  \
nvcr.io/nvidia/tritonserver:22.04-py3 tritonserver --model-repository=/models \
--strict-model-config=false --grpc-infer-allocation-pool-size=16 --log-verbose 1
```

## Client

### Check Triton Server Connection

```bash
curl -v http://localhost:8000/v2/health/ready
```

### Check Model Config

```bash
curl localhost:8000/v2/models/<your model name>/config
```

### Run Triton Client Docker
```bash
docker run --gpus all -it  \
--privileged --network host -v /dev:/dev --ipc=host --shm-size=1g  -v /tmp/.X11-unix:/tmp/.X11-unix \
-e DISPLAY=$DISPLAY   nvcr.io/nvidia/tritonserver:22.04-py3-sdk
```
 
