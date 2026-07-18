FROM rocm/pytorch:rocm7.2_ubuntu24.04_py3.12_pytorch_release_2.10.0

ARG COMFYUI_VERSION=v0.28.0

USER root

RUN apt-get update \
    && apt-get install --yes --no-install-recommends git \
    && rm -rf /var/lib/apt/lists/*

RUN python3 -m pip install --no-cache-dir --upgrade pip \
    && python3 -m pip uninstall --yes torch torchvision torchaudio \
    && python3 -m pip install --no-cache-dir --pre \
        --index-url https://rocm.nightlies.amd.com/v2/gfx1151/ \
        torch torchvision torchaudio

WORKDIR /workspace

RUN git clone --branch "${COMFYUI_VERSION}" --depth 1 \
        https://github.com/Comfy-Org/ComfyUI.git ComfyUI \
    && python3 -m pip install --no-cache-dir -r ComfyUI/requirements.txt

WORKDIR /workspace/ComfyUI

ENV PYTORCH_TUNABLEOP_ENABLED=1

EXPOSE 8188

CMD ["python3", "main.py", "--listen", "0.0.0.0", "--port", "8188", "--enable-manager"]
