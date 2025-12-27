# **Qwen-Image-Edit-2511-LoRAs-Fast-Single-Image-Rerun**

> A Gradio-based experimental demonstration for the Qwen/Qwen-Image-Edit-2511 model with lazy-loaded LoRA adapters for single-image editing tasks. Features specialized edits like photo-to-anime conversion and multi-angle transformations. Unique integration with Rerun SDK: outputs are visualized in an interactive 3D-aware viewer, logging both original and edited images as side-by-side comparisons in a saved .rrd file.

## Features

- **Single-Image Editing**: Upload one image and apply edits via natural language prompts (e.g., "transform into anime").
- **Lazy LoRA Loading**: 2 adapters (Photo-to-Anime, Multiple-Angles) load on-demand to save memory.
- **Rerun Visualization**: Uses `gradio-rerun` and `rerun-sdk` to display original and edited images in an interactive viewer; saves recordings as `.rrd` files in `tmp_rerun/`.
- **Rapid Inference**: Flash Attention 3 enabled; 4-step default generations with bfloat16.
- **Auto-Resizing**: Maintains aspect ratio up to 1024px max edge (multiples of 8).
- **Custom Theme**: OrangeRedTheme with gradients for a modern interface.
- **Queueing Support**: Up to 30 concurrent jobs with error handling.

**Note**: This is an experimental Space for the newer Qwen-Image-Edit-2511 model. For stable performance, consider the [Qwen-Image-Edit-2509 version](https://huggingface.co/spaces/prithivMLmods/Qwen-Image-Edit-2509-LoRAs-Fast).

## Prerequisites

- Python 3.10 or higher.
- CUDA-compatible GPU (required for bfloat16 and Flash Attention 3).
- Stable internet for initial model/LoRA downloads.

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/PRITHIVSAKTHIUR/Qwen-Image-Edit-2511-LoRAs-Fast-Single-Image-Rerun.git
   cd Qwen-Image-Edit-2511-LoRAs-Fast-Single-Image-Rerun
   ```

2. Install dependencies:
   Create a `requirements.txt` file with the following content, then run:
   ```
   pip install -r requirements.txt
   ```

   **requirements.txt content:**
   ```
   git+https://github.com/huggingface/accelerate.git
   git+https://github.com/huggingface/diffusers.git
   git+https://github.com/huggingface/peft.git
   transformers==4.57.3
   huggingface_hub
   sentencepiece
   gradio-rerun
   torchvision
   supervision
   rerun-sdk
   kernels
   spaces
   hf_xet
   torch
   numpy
   av
   ```

3. Start the application:
   ```
   python app.py
   ```
   The demo launches at `http://localhost:7860`.

## Usage

1. **Upload Image**: Select a single image (height up to 290px preview).

2. **Select Adapter**: Choose "Photo-to-Anime" or "Multiple-Angles".

3. **Enter Prompt**: Describe the edit (e.g., "transform into anime" or "rotate camera 45 degrees left").

4. **Edit Image**: Click "Edit Image".

5. **Output**:
   - Interactive Rerun viewer showing original and edited images.
   - Recording saved as `.rrd` in `tmp_rerun/` (UUID-named).

### Supported Adapters

| Adapter           | Use Case                          |
|-------------------|-----------------------------------|
| Photo-to-Anime   | Realistic to anime style transfer |
| Multiple-Angles  | Camera angle/viewpoint changes    |

## Rerun Viewer

- Displays "images/original" and "images/edited" paths.
- Supports pan, zoom, and timeline if extended.
- Files persist in `tmp_rerun/` until manually cleared.

## Troubleshooting

- **Rerun Errors**: Ensure `gradio-rerun` and `rerun-sdk` installed; fallback handles SDK version differences.
- **Adapter Loading**: First use downloads LoRA; check console for progress.
- **OOM**: Reduce steps/resolution; clear cache with `torch.cuda.empty_cache()`.
- **Flash Attention Fails**: Fallback to default attention; requires compatible CUDA.
- **No Output**: Ensure image uploaded and prompt valid.
- **Queue Full**: Increase `max_size` in `demo.queue()`.

## Contributing

Contributions welcome! Fork the repo, add new adapters to `ADAPTER_SPECS`, enhance Rerun logging (e.g., tensors, masks), or improve prompts, and submit PRs with tests.

Repository: [https://github.com/PRITHIVSAKTHIUR/Qwen-Image-Edit-2511-LoRAs-Fast-Single-Image-Rerun.git](https://github.com/PRITHIVSAKTHIUR/Qwen-Image-Edit-2511-LoRAs-Fast-Single-Image-Rerun.git)

## License

Apache License 2.0. See [LICENSE](LICENSE) for details.

Built by Prithiv Sakthi. Report issues via the repository.
