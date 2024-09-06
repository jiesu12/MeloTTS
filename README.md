## Install

```
git clone https://github.com/myshell-ai/MeloTTS.git
cd MeloTTS
pip install -e .
python -m unidic download
```

Run Python, in Python console:

```
>>> import nltk
>>> nltk.download('averaged_perceptron_tagger_eng')
```
It will create a folder `~/nltk_data`, which will be used by MeloTTS during TTS.

Disable Windows max path length limit. See - <https://learn.microsoft.com/en-us/windows/win32/fileio/maximum-file-path-limitation?tabs=registry>. When install Python on Windows, the installer can fix the limit for you.

## Run Web Server

```
python ./melo/app.py
```
Then open <http://127.0.0.1:7860/>.

## Run Command Line

```
python ./melo/main.py --language 'ZH' --speed 0.9 "你好" output.wav
python ./melo/main.py --language 'ZH' --speed 0.9 --file test.txt output.wav
```