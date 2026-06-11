> **This repository is archived. No further updates will be made.**
>
> The Matxa Catalan multispeaker/multidialect voices have been absorbed into [phoonnx](https://github.com/TigreGotico/phoonnx), a unified ONNX TTS plugin that uses the same models with an improved inference engine. Migrate using the guide below.

# ovos-tts-plugin-matxa-multispeaker-cat → phoonnx migration

## Install

```bash
pip install phoonnx
```

`espeak-ng` with Catalan support is required (same as before). Depending on your distro you may need to compile from source — see the [espeak-ng Catalan PR](https://github.com/espeak-ng/espeak-ng/pull/1681).

## Voice mapping

phoonnx ships several variants of the Matxa model. The recommended replacement for the old plugin is `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage`, which uses the same acoustic model with the alVoCat (Vocos) vocoder — the same vocoder the original plugin used.

| Old voice | phoonnx voice id | Notes |
|-----------|-----------------|-------|
| `balear/quim` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` + `speaker_id: 0` | |
| `balear/olga` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` + `speaker_id: 1` | |
| `central/grau` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` + `speaker_id: 2` | default |
| `central/elia` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` + `speaker_id: 3` | |
| `nord-occidental/pere` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` + `speaker_id: 4` | |
| `nord-occidental/emma` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` + `speaker_id: 5` | |
| `valencia/lluc` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` + `speaker_id: 6` | |
| `valencia/gina` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` + `speaker_id: 7` | |

Additional Matxa variants available in phoonnx:

| Voice id | Description |
|----------|-------------|
| `OpenVoiceOS/matxa-cat-multispeaker-wavenext` | End-to-end (wavenext vocoder baked in) |
| `OpenVoiceOS/matxa-cat-multispeaker-hifigan` | HiFi-GAN vocoder |
| `OpenVoiceOS/matxa-cat-multiaccent-wavenext` | Multiaccent variant |
| `OpenVoiceOS/matxa-cat-central-graphemes-v2` | Grapheme-based (no espeak-ng required) |
| `OpenVoiceOS/matxa-cat-multispeaker-wavenext-2stage` | Two-stage with WaveNext vocoder |

## Configuration mapping

**Before:**
```json
"tts": {
  "module": "ovos-tts-plugin-matxa-multispeaker-cat",
  "ovos-tts-plugin-matxa-multispeaker-cat": {
    "voice": "valencia/gina"
  }
}
```

**After:**
```json
"tts": {
  "module": "phoonnx",
  "phoonnx": {
    "voice": "OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage",
    "speaker_id": 7
  }
}
```

### Auto-select by language

Set your OVOS language to `ca`, `ca-ba`, `ca-va`, or `ca-nw` and leave `voice` unset — phoonnx will select the appropriate Matxa dialect variant automatically.

## Credits

Original plugin by the OpenVoiceOS community.
🍵 [Matxa-TTS](https://huggingface.co/projecte-aina/matxa-tts-cat-multiaccent) and 🥑 [alVoCat](https://huggingface.co/projecte-aina/alvocat-vocos-22khz) by Projecte AINA.

![img.png](img.png)
> This plugin was funded by the Ministerio para la Transformación Digital y de la Función Pública and Plan de Recuperación, Transformación y Resiliencia - Funded by EU – NextGenerationEU within the framework of the project ILENIA with reference 2022/TL22/00215337

![img_1.png](img_1.png)
> 🍵 Matxa-TTS and 🥑 alVoCat were funded by the Generalitat de Catalunya within the framework of [Projecte AINA](https://politiquesdigitals.gencat.cat/ca/economia/catalonia-ai/aina).
