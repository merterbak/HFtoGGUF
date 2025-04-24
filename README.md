# HFtoGGUF
Convert Hugging Face models to GGUF with xet support.

## Features
- Clones and builds `llama.cpp` using CMake in Colab.
- Downloads models from Hugging Face using `huggingface_hub`.
- Converts Hugging Face models to 16-bit GGUF format.
- Quantizes models to specified levels (e.g., Q3_K_S, Q4_0, etc.).
- Uploads quantized models to a new or existing Hugging Face repository.
- Inference support for running quantized models.

## Configuration

Modify the following variables in the notebook for your own needs:

- model_name: The Hugging Face model to download (e.g., meta-llama/Llama-3.2-3B-Instruct).
- quant_levels: List of quantization levels (e.g., ["Q3_K_S"]).
- new_repo_name: The Hugging Face repository for uploading quantized models (e.g., your-username/Llama-3.2-3B-Instruct-GGUF).
- local_dir: Directory to store models (default: ./model).
  
To enable GPU acceleration for inference in Google Colab:

1. Make sure your Colab runtime is set to **GPU**:  
   Go to `Runtime > Change runtime type > Hardware accelerator > GPU`.

2. Uncomment and run the following GPU-specific CMake commands in a notebook cell:

```bash
!cmake -B build -DGGML_CUDA=ON
!cmake --build build --config Release
```
If you have xet early access download xet version of it. If your Python environment has a hf_xet-aware version of huggingface_hub then your uploads and downloads will automatically use Xet.
```bash
!pip install -U huggingface_hub[hf_xet]
```

