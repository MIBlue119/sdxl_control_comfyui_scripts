# SDXL Control ComfyUI Scripts

Just a script to 
- Make docker image and docker container 
- Support SDXL/control net 
- Run the [ComfyUI](https://github.com/comfyanonymous/ComfyUI)

## Resources
- Stability/Control-lora:https://huggingface.co/stabilityai/control-lora
- HuggingFace's online ComfyUI demo: https://huggingface.co/spaces/SpacesExamples/ComfyUI
- Stable Diffusion Prompt Book: https://cdn.openart.ai/assets/Stable%20Diffusion%20Prompt%20Book%20From%20OpenArt%2010-28.pdf

## Support Environment
- Linux
- nvidia GPU with more than 20 G Vram
- Harddrive more than 100GB
## Installation

0. Prepare the basic environment
- docker engine: https://docs.docker.com/engine/install/ubuntu/
- nvidia container toolkit: https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html


1. Build the docker image
```
docker build -f Dockerfile -t sdxl_comfyui .
```

2. Download related models(sdxl/controlnet/vae/upscale models)
- `models` is embty and the structure is from [ComfyUI](https://github.com/comfyanonymous/ComfyUI)
- the script is based on huggingfaces' example: https://huggingface.co/spaces/SpacesExamples/ComfyUI/blob/main/Dockerfile
```
./prepare_sdxl_models.sh
```

3. Run the container
- Run a container and remove after exit, the port is on 5566. After running, open [localhost:5566](localhost:5566) with browser
```
sudo docker run --gpus=0 --rm -p5566:5566  -v ${PWD}/models:/home/user/app/models -v ${PWD}/output:/home/user/app/output sdxl_comfyui 
```

4. Open the example workflow from the GUI button `Open`
- The folder `workflow` contains example workflows to run control-canny/control-depth/control-sketch/control-recolor
- There are some test datas under `test_datas`
