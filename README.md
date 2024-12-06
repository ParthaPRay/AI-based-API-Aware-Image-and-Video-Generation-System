# AI-based-API-Aware-Image-and-Video-Generation-System
This repo contains code and instructions for AI-based API Aware Image and Video Generation System

# AI-based API Aware Image and Video Generation System

This project provides a workflow for generating AI-driven, API-aware images and videos based on text prompts, storing the generated content and logs in databases, and serving the results through a web interface.

---

## Overview

### 1. Text-to-Image and Text-to-Video Generation

Using OpenAI’s DALL·E 3 and RunwayML’s video generation model, this system takes a user prompt and generates 5 images and 5 corresponding videos.

- The `image_video_generation.py` code uses a user-provided text prompt to generate images via the DALL·E 3 image generator. 
- Each generated image is saved in `generated_content/<user_id>` as `image_1.png`, and so on.
- Each image is then converted to Base64 format and, along with the text prompt, sent to the RunwayML API to generate a 5-second video. This video is saved in the same directory as the corresponding image (e.g., `video_1.mp4`).

**Note:** More images and videos can be generated by changing the `n` parameter in the `generate_images_and_videos()` function. However, this may incur significant costs.

```python
generate_images_and_videos(user_id, prompt, n=5, image_size="1024x1024", video_duration=5)
