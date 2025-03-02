# Kobold API STT Component

## What is this for?

This is a speech-to-text component for Project J.A.I.son that uses the locally-runnable [Kobold C++](https://github.com/LostRuins/koboldcpp) API to use their STT models.

## Setup

Download the latest release for your system from [Kobold C++'s repository](https://github.com/LostRuins/koboldcpp/releases) (get the latest `.exe` that corresponds to your system, for example `koboldcpp_cu12.exe` for Windows with NVidia GPU). Also download one of the models from [HuggingFace](https://huggingface.co/ggerganov/whisper.cpp/tree/main). `ggml-base-q5_1.bin` is recommended.

Open the downloaded executable. On the first page, check that your using the right device (ideally your GPU). 

<img src="./assets/initial_conf.png" alt="Changes on main page" height="400"/>

Navigate to Audio, then search and add your downloaded model.

<img src="./assets/audio_conf.png" alt="Adding model in config" height="200"/>

Remember to save your configuration and make note of its filepath.

Now setup this project's environment:

Windows
```
conda create -n jaison-comp-stt-kobold python=3.12
conda activate jaison-comp-stt-kobold
pip install -r requirements.txt
```

Unix
```
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

## Testing
Assuming you are in the right virtual environment and are in the root directory:
```
python ./src/main.py --port=5000
```
If it runs, it should be fine.

## Configuration

Configurables found in `config.yaml`. Below are the descriptions of the configurables. See notes below that.

- `endpoint`: (str) url to existing Kobold API endpoint
- `kobold-filepath`: (str) if no existing endpoint, filepath to Kobold executable
- `kcpps-filepath`: (str) if no existing endpoint, filepath to Kobold config to start with
- `force-port`: (str) if no existing endpoint, force component-started endpoint to run on this port
`prompt`: (str) Initial prompt to help with spelling and context
`suppress-non-speech`: (bool) Whether to skip non-speech sounds
`langcode`: (str) Language code
`use-vulkan`: (bool) Use Vulkan for running models. Make false if you're having issues with Vulkan.
`vulkan-device`: (str) Specify a specific device id for Vulkan acceleration. `null` for auto-detect

**Notes:** You only really need to fill out `endpoint` or both of `kobold-filepath` and `kcpps-filepath`. Everything else is specific to you and what you're trying to do. In most cases, the defaults are fine.

Also remember, **if your on Windows**, replace every `\` with `\\` for filepaths.

## Related stuff

Project J.A.I.son: https://github.com/limitcantcode/jaison-core

Join the community Discord: https://discord.gg/Z8yyEzHsYM
