# Lipsyncing with Translated Audio

This project demonstrates an end-to-end pipeline for lip-syncing videos with translated audio, enabling multilingual accessibility and enhanced video editing capabilities. The pipeline involves extracting audio from a video, enhancing the audio quality, transcribing and translating the audio, generating synthesized speech, and lip-syncing the translated audio to the original video.
https://colab.research.google.com/drive/1yvqbgZZPMlCcXi8nk9ItxzY2Nk7-3Gfs?usp=sharing

---

## Features

- **Audio Extraction**: Converts video files to audio files in MP3 format using MoviePy.
- **Audio Enhancement**: Cleans and enhances audio quality using the Spectral Mask Enhancement model.
- **Speech-to-Text Transcription**: Transcribes audio to text using OpenAI's Whisper model.
- **Language Translation**: Translates text into the desired language using IndicTrans2.
- **Speech Synthesis**: Generates high-quality speech audio from translated text using gTTS or a multilingual TTS model.
- **Voice Conversion**: Clones voice characteristics to match the original speaker using multilingual voice cloning models.
- **Lip Syncing**: Uses the Wav2Lip GAN model to synchronize the translated audio with the speaker's lip movements in the original video.

---

## Requirements

Install the following dependencies:

- Python 3.8+
- Required Python libraries:
  ```bash
  pip install moviepy torch torchaudio gtts TTS whisper
  ```
- Additional tools and models:
  - [IndicTrans2](https://github.com/AI4Bharat/IndicTrans2)
  - [Wav2Lip](https://github.com/zabique/Wav2Lip)

---

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/lipsync-translated-audio.git
   cd lipsync-translated-audio
   ```

2. Install required libraries:
   ```bash
   pip install -r requirements.txt
   ```

3. Download pretrained models:
   - [Wav2Lip GAN model](https://iiitaphyd-my.sharepoint.com/.../wav2lip_gan.pth)
   - [Face detection model](https://www.adrianbulat.com/.../s3fd.pth)

---

## Usage

### Step 1: Extract Audio from Video
Convert the video file to an MP3 audio file:
```python
from moviepy.editor import VideoFileClip

def mp4_to_mp3(mp4file, mp3file):
    videoclip = VideoFileClip(mp4file)
    audioclip = videoclip.audio
    audioclip.write_audiofile(mp3file)
    audioclip.close()
    videoclip.close()
```

### Step 2: Enhance Audio Quality
Use the `SpectralMaskEnhancement` model to clean and enhance audio:
```python
import torchaudio
from speechbrain.inference.enhancement import SpectralMaskEnhancement

enhance_model = SpectralMaskEnhancement.from_hparams(
    source="speechbrain/metricgan-plus-voicebank",
    savedir="pretrained_models/metricgan-plus-voicebank"
)
noisy_audio = enhance_model.load_audio(audio_file).unsqueeze(0)
enhanced_audio = enhance_model.enhance_batch(noisy_audio)
torchaudio.save("enhanced_audio.wav", enhanced_audio.cpu(), 16000)
```

### Step 3: Transcribe Audio
Transcribe audio to text using Whisper:
```python
import whisper

model = whisper.load_model("medium.en")
transcription = model.transcribe("enhanced_audio.wav")['text']
```

### Step 4: Translate Text
Translate the transcription to the desired language using IndicTrans2:
```python
from IndicTransTokenizer import IndicProcessor, IndicTransTokenizer

tokenizer, model = initialize_model_and_tokenizer("ai4bharat/indictrans2-en-indic-1B", "en-indic", None)
processor = IndicProcessor(inference=True)
translated_text = batch_translate([transcription], "eng_Latn", "hin_Deva", model, tokenizer, processor)
```

### Step 5: Generate Speech
Use `gTTS` or the `TTS` library to synthesize speech:
```python
from gtts import gTTS

tts = gTTS(text=translated_text[0], lang='hi')
tts.save("translated_audio.mp3")
```

### Step 6: Lip Sync Video
Use Wav2Lip GAN to sync the translated audio with the original video:
```bash
python /content/Wav2Lip/inference.py --checkpoint_path /content/Wav2Lip/checkpoints/wav2lip_gan.pth --face "/content/video.mp4" --audio "/content/translated_audio.mp3" --outfile "/content/output_video.mp4"
```

---

## Results

- The final output is a video with the speaker's lips synced to the translated and synthesized audio, enabling effective communication in multiple languages.
- ![image](https://github.com/user-attachments/assets/f24f7660-65b7-4a11-ab09-dad9d62034b7)
- 


---

## Acknowledgments

- **IndicTrans2**: AI4Bharat's translation models for Indian languages.
- **Wav2Lip**: Real-time lip-syncing using GANs.
- **SpeechBrain**: Pretrained models for audio enhancement.
