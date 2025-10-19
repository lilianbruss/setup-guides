# OpenCV Installation


[OpenCV](https://opencv.org/) is a popular Python package for computer vision and image processing tasks. It provides tools for working with images, video streams, facial recognition, feature detection, and more.

You can install OpenCV using any Python package manager. In this guide, we’ll use [`uv`](https://github.com/astral-sh/uv) within a virtual environment to manage the installation.

---

## Activate Your Virtual Environment

If you've already created a virtual environment with `uv`, activate it:
- `source .venv/bin/activate`

Add either of these OpenCV Python libraries to your uv environment (only **one**):

- `uv add opencv-python` (basic package)
- `uv add opencv-contrib-python` (additional modules like `cv2.face`)
- `uv add opencv-python-headless`(headless version does not support GUI modules like `cv2.imshow` for notebooks or video display code)


## Missing GUI Support (Linux)

If you're using one of the full versions (not headless), you might encounter an error about missing libraries such as `libGL.so.1` This is required for GUI functions like image and video display.

To fix this and enable OpenCV's GUI features, install the following system packages:
- `sudo apt update`
- `sudo apt-get install ffmpeg libsm6 libxext6  -y`

## Verifying Installation

Test out your new package in a Python file:

```ruby
import cv2

print(cv2.__version__)
```