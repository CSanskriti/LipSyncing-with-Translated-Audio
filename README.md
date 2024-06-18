# LipSyncing with Translated Audio

LipSyncing with Translated Audio is a project aimed at enhancing and translating audio from videos, performing voice cloning, and synchronizing the translated audio with the original video through lip syncing. This repository provides scripts and tools to automate these tasks, making it easier to process and create videos with translated audio synced to the speaker's lip movements.

## Table of Contents

- [Project Overview](#project-overview)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
  - [Running the Streamlit App](#running-the-streamlit-app)
- [Configuration](#configuration)
- [Examples](#examples)
- [Contributing](#contributing)
- [License](#license)

## Project Overview

The project consists of several Python scripts and a Streamlit web application that automate the following tasks:

1. **Audio Extraction**: Extracting audio from input video files.
2. **Audio Enhancement**: Enhancing audio quality using a spectral enhancement model.
3. **Audio Translation**: Translating the extracted audio to multiple languages using machine translation.
4. **Voice Cloning**: Cloning the speaker's voice using Text-to-Speech (TTS) and Voice Conversion (VC) models.
5. **Lip Syncing**: Synchronizing the translated audio with the original video's lip movements.
6. **Streamlit App**: Providing an interactive web interface for users to upload videos and view processed results.

## Project Structure

The project is structured as follows:

```
LipSyncing-with-Translated-Audio/
├── README.md
├── requirements.txt
├── streamlit_app.py
├── audio_extraction.py
├── audio_enhancement.py
├── audio_translation.py
├── voice_cloning.py
├── lipsyncing.py
└── data/
    ├── input_videos/
    ├── output_videos/
    └── ...
```

- **`README.md`**: This file, providing an overview of the project and instructions for usage.
- **`requirements.txt`**: Lists dependencies required to run the project.
- **`streamlit_app.py`**: Script for the Streamlit web application.
- **`audio_extraction.py`**: Script to extract audio from input videos.
- **`audio_enhancement.py`**: Script for enhancing audio quality.
- **`audio_translation.py`**: Script to translate audio using machine translation.
- **`voice_cloning.py`**: Script for voice cloning using TTS and VC models.
- **`lipsyncing.py`**: Script for performing lip syncing of translated audio with video.
- **`data/`**: Directory for storing input and output video files.

## Installation

To run the project, follow these steps:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/CSanskriti/LipSyncing-with-Translated-Audio.git
   cd LipSyncing-with-Translated-Audio
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Download pre-trained models and data files as needed.**

## Usage

### Running the Streamlit App

1. Navigate to the project directory:
   ```bash
   cd LipSyncing-with-Translated-Audio
   ```

2. Run the Streamlit app:
   ```bash
   streamlit run streamlit_app.py
   ```

3. Upload your video file through the Streamlit interface and follow the instructions to process and view results.

## Configuration

No special configuration files are needed beyond ensuring dependencies are installed and models are downloaded as specified in the installation instructions.

## Examples



## Contributing

Contributions are welcome! If you wish to contribute to this project, please follow these guidelines:
- Fork the repository, make changes, and submit a pull request.
- For major changes, please open an issue first to discuss what you would like to change.

