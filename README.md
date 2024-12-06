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
```

- Images: Stored in generated_content/<user_id>/image_x.png.
- Videos: Stored in generated_content/<user_id>/video_x.mp4.

### 2. Storing and Managing Content

The generated content details (prompts, file paths, status, timestamps) are stored in a database (ai_generation.db). Once generation is complete, the status is updated to "Completed."


### 3. User Access and Web Page Display

A Flask web application (web.py) allows users to access their generated images and videos by providing a user_id.

- If the content is still processing, a "Processing" page is displayed.
- Once completed, a gallery of images and playable videos is shown.

User actions (login attempts and content views) are logged in a separate database (user_logs.db).

### 4. Notifications

When content generation is complete, the system prints a notification message to the terminal, including a link to the web page where the user can view their content.

### 5. Directory Structure

![image](https://github.com/user-attachments/assets/bce102f4-0b53-44c0-8c13-c2d0774f1a40)


- generated_content/: Holds generated images and videos for each user.
- templates/: Contains HTML templates for the gallery and processing pages.
- main.py: CLI script to trigger generation and send notification once done.
- web.py: Flask web application serving the generated content and logging user actions.
- database.py: Manages the ai_generation.db for storing user content and metadata.
- config.py: Loads environment variables and configuration.
- image_video_generation.py: Contains functions for generating images and videos.
- notifications.py: Handles user notifications (in-terminal message).
- requirements.txt: Lists Python dependencies.
- .env: Contains API keys and other secrets (not checked into version control).

### 6. Prerequisites

- Python 3.11.2
- A .env file with the following variables:

```bash
  OPENAI_API_KEY=<your_openai_api_key>
  RUNWAYML_API_SECRET=<your_runwayml_api_key>
```
