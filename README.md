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
Or use `~/.local/bin/melo-ui`:
```
melo-ui
```

Then open <http://127.0.0.1:7860/>.


## Run Command Line

```
python ./melo/main.py --language 'ZH' --speed 0.9 "你好" output.wav
python ./melo/main.py --language 'ZH' --speed 0.9 --file test.txt output.wav
```

Or use  `~/.local/bin/melo`:
```
melo --language 'ZH' --speed 0.9 "你好" output.wav
```

Batch:
```
for f in `ls *.txt`;do if ! [[ -f $f.wav ]];then echo $f;melo --language 'ZH' --speed 0.9 --file $f $f.wav;fi;done
```

## Training

```
mkdir -p ~/tmp/jie
cp melo/data/example/jie/metadata.list ~/tmp/jie
# copy *.wav files to ~/tmp/jie
cd melo
python ./melo/preprocess_text.py --metadata /home/jie/tmp/jie/metadata.list --config_path /home/jie/project/MeloTTS/melo/configs/config.json
```
A `config.json` will be generated in `/home/jie/tmp/jie/`

```
bash train.sh /home/jie/tmp/jie/config.json 1
```

`train.sh` runs a infinite loop, need to Ctrl-C to stop it. For each iteration, a `pth` files is created in `MeloTTS/melo/logs/jie/G_<iteration>000.pth`. The result gets better as more iterations are run.

The time took to finish one training iteration using 20 wav files was about one hour.

### Inference

```
cd melo
python infer.py --text "some text here" -m ./logs/jie/G_<iteration>000.pth -o <output_dir>
```
