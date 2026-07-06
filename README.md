ImaGen Remastered

A local AI image generation setup built on ComfyUI + FLUX.1 Dev FP8 + PuLID Flux, focused on photorealistic image generation with identity preservation.

Features
FLUX.1 Dev FP8 image generation
Local execution (no API required)
RTX 4050 Laptop GPU compatible (6GB VRAM)
PuLID Flux identity preservation
ComfyUI workflow-based pipeline
GitHub backed reproducible setup
HuggingFace model integration
System Used
Component	Specification
GPU	RTX 4050 Laptop GPU (6GB)
CPU	Ryzen 7 7435HS
RAM	16GB DDR5
OS	Windows 11
Python	3.10.x
CUDA	12.8
Torch	2.11.0+cu128
Installation
Create Virtual Environment
python -m venv venv
.\venv\Scripts\activate
Clone ComfyUI
git clone https://github.com/comfyanonymous/ComfyUI.git
cd ComfyUI
Install Requirements
pip install -r requirements.txt
Replace CPU Torch (if installed)
pip uninstall -y torch torchvision torchaudio
Install CUDA Build
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128
Model Downloads
FLUX.1 Dev FP8
pip install -U "huggingface_hub[cli]"

mkdir models\diffusion_models

hf download Comfy-Org/flux1-dev flux1-dev-fp8.safetensors --local-dir models\diffusion_models
CLIP

Place:

clip_l.safetensors
t5xxl_fp8_e4m3fn.safetensors

inside:

ComfyUI\models\clip
VAE

Place:

ae.safetensors

inside:

ComfyUI\models\vae
PuLID Setup

Install:

ComfyUI-PuLID-Flux-GR

Required models:

pulid_flux_v0.9.0.safetensors
EVA CLIP
InsightFace
Workflow

Current stable workflow:

FLUX.1 Dev FP8
↓
PuLID Flux GR
↓
Basic Guider
↓
Euler Sampler
↓
VAE Decode
↓
Output Image
Recommended Settings
FLUX
Sampler: Euler
Scheduler: Simple
Steps: 20
Resolution: 1024x1024
PuLID
Weight: 0.45 - 0.50
Blur: 0.01
Train Step: 1000
Use Gray: Disabled
Known Issues
PuLID Weight > 0.5

Current setup becomes unstable above:

Weight: 0.5

Potential causes:

VRAM limitation (RTX 4050 6GB)
ComfyUI memory streaming
PuLID compatibility with newer ComfyUI versions
Project Structure
ImaGen/
│
├── ComfyUI/
├── workflows/
│   └── ImaGen.json
├── checkpoint2_requirements.txt
├── notes
└── .gitignore
Export Requirements
pip freeze > checkpoint2_requirements.txt
Launch
.\venv\Scripts\activate

cd ComfyUI

python main.py

Open:

http://127.0.0.1:8188
Credits
ComfyUI
Black Forest Labs (FLUX)
PuLID
InsightFace
HuggingFace
Status

✅ FLUX Working
✅ ComfyUI Working
✅ GitHub Backup Complete
✅ PuLID Functional
⚠️ High-weight PuLID Optimization Pending
