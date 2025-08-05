~~~python
pip install git+https://github.com/openai/whisper.git
pip install torchaudio
~~~

~~~python 
/stt-project/
├── samples/
│   ├── turkmen1.wav
│   └── turkmen2.wav
├── transcribe.py
~~~

~~~python 
ffmpeg -i input.mp3 -ar 16000 -ac 1 samples/turkmen1.wav
~~~

transcribe.py
~~~python 
import whisper
import os

model = whisper.load_model("base")  # or "small", "medium", "large"

audio_dir = "samples"

for filename in os.listdir(audio_dir):
    if filename.endswith(".wav"):
        path = os.path.join(audio_dir, filename)
        print(f"\n🔊 Transcribing: {filename}")
        result = model.transcribe(path, language="tk")  # "tk" = Turkmen
        print("📝 Transcript:", result["text"])

~~~

for my own 
### 1. 📁 **Prepare Dataset**

You need a large dataset with:

- `.wav` files (16kHz, mono recommended)
    
- Matching transcripts (in `.txt`, `.csv`, or `.json`)

~~~arduino
/data/
  ├── audio/
  │     ├── 001.wav
  │     ├── 002.wav
  └── transcriptions.csv
        ┌──────────┬────────────────────┐
        │ file     │ text               │
        ├──────────┼────────────────────┤
        │ 001.wav  │ salam dostlarym    │
        │ 002.wav  │ men bararyn        │
        └──────────┴────────────────────┘
~~~

### 2. 🧠 Choose a Model Architecture

Start with one of these:

- `wav2vec 2.0` (by Meta)
    
- `QuartzNet`, `Conformer`, or `DeepSpeech` (by Mozilla)
    

🟢 I recommend **wav2vec 2.0** if you want SOTA accuracy.

	1. 🧪 Preprocess Audio

~~~bash
ffmpeg -i input.amr -ar 16000 -ac 1 output.wav
~~~

~~~bash
for f in *.amr; do
  ffmpeg -i "$f" -ar 16000 -ac 1 "${f%.amr}.wav"
done
~~~

4. 🛠️ Install Tools
~~~bash
pip install torchaudio transformers datasets jiwer
~~~


