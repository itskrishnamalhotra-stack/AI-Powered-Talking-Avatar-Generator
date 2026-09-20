# AI-Powered Talking Avatar Generator

A modular generative-video pipeline that converts one portrait and an audio recording into a high-resolution, lip-synchronised talking-avatar video.

> Built in 2025 and designed around Google Colab GPU constraints.

## Pipeline

1. **Transcription** — Whisper converts the audio into timestamped segments.
2. **Motion planning** — Gemini turns the transcript into visual action and expression prompts.
3. **Video generation** — Wan 2.1 generates short clips while the previous clip's final frame helps maintain continuity.
4. **Composition** — MoviePy joins the generated segments.
5. **Lip synchronisation** — Wav2Lip aligns mouth motion with the original speech.
6. **Enhancement** — Real-ESRGAN optionally upscales and restores detail.

## Why the workflow is split into sessions

Running transcription, diffusion/video generation, lip-sync and super-resolution together can exceed a free Colab runtime's memory. The project separates these stages so intermediate assets can be saved and each model can be loaded independently.

## Repository layout

| Notebook | Responsibility |
| --- | --- |
| `Session_1_(Audio_to_Segment).ipynb` | Transcription and timestamp preparation |
| `Session_2_(Image_to_Video).ipynb` | Prompt planning and video generation |
| `Session_3_(Video_and_Audio_to_Lipsync).ipynb` | Wav2Lip inference |
| `Session_4_(Enhance_the_Video_using_ESRGAN_(Optional)).ipynb` | Optional super-resolution |

## Tech stack

Python · PyTorch · Whisper · Gemini API · Wan 2.1 · ComfyUI · Wav2Lip · Real-ESRGAN · FFmpeg · MoviePy · OpenCV

## Running it

Open the notebooks in Colab and execute them in numerical order. API credentials and personal Drive paths are intentionally excluded. Configure credentials through Colab Secrets or environment variables rather than placing them inside a notebook.

## Current limitations

- The workflow is notebook-based rather than a single packaged application.
- Model URLs and dependencies may need updating as upstream projects change.
- Identity and temporal consistency depend on the selected checkpoint and source image.
- Generated media should only be created with appropriate consent and usage rights.

## Status

Research and portfolio prototype demonstrating multi-model orchestration under limited GPU memory.
