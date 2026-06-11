> **This repository is archived. No further updates will be made.**
>
> The Matxa Catalan multispeaker/multidialect voices have been absorbed into [phoonnx](https://github.com/TigreGotico/phoonnx), a unified ONNX TTS plugin that uses the same models with an improved inference engine. Migrate using the guide below.

# ovos-tts-plugin-matxa-multispeaker-cat → phoonnx migration

## Install

```bash
pip install phoonnx
```

`espeak-ng` with Catalan support is required (same as before). Depending on your distro you may need to compile from source — see the [espeak-ng Catalan PR](https://github.com/espeak-ng/espeak-ng/pull/1681).

Alternatively, use `OpenVoiceOS/matxa-cat-central-graphemes-v2` which requires no espeak-ng.

## Voice mapping

The direct equivalent of the old plugin is `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` — same acoustic model, same alVoCat/Vocos vocoder. Select speakers via `speaker_id`:

| Old voice | phoonnx voice id | `speaker_id` |
|-----------|-----------------|-------------|
| `balear/quim` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` | `0` |
| `balear/olga` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` | `1` |
| `central/grau` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` | `2` |
| `central/elia` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` | `3` |
| `nord-occidental/pere` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` | `4` |
| `nord-occidental/emma` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` | `5` |
| `valencia/lluc` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` | `6` |
| `valencia/gina` | `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` | `7` |

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
  "module": "ovos-tts-plugin-phoonnx",
  "ovos-tts-plugin-phoonnx": {
    "voice": "OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage",
    "speaker_id": 7
  }
}
```

### Auto-select by language

Set your OVOS language to `ca`, `ca-ba`, `ca-va`, or `ca-nw` and leave `voice` unset — phoonnx will select the appropriate Matxa dialect variant automatically.

## Other available Matxa variants

| Voice ID | Vocoder | Notes |
|----------|---------|-------|
| `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` | alVoCat/Vocos | Recommended — closest to original plugin |
| `OpenVoiceOS/matxa-cat-multispeaker-wavenext-2stage` | WaveNext | Two-stage with WaveNext vocoder |
| `OpenVoiceOS/matxa-cat-multispeaker-wavenext` | WaveNext (baked in) | End-to-end, no separate vocoder |
| `OpenVoiceOS/matxa-cat-multispeaker-hifigan` | HiFi-GAN | End-to-end |
| `OpenVoiceOS/matxa-cat-multiaccent-wavenext` | WaveNext | Multiaccent variant |
| `OpenVoiceOS/matxa-cat-central-graphemes-v2` | — | Grapheme-based, no espeak-ng required |

## Voice catalogue

All available Catalan voices (and every other supported voice) are listed in [VOICES.md](https://github.com/TigreGotico/phoonnx/blob/dev/VOICES.md) — that is the canonical reference for voice IDs to use in your config.

Set your OVOS language to `ca`, `ca-ba`, `ca-va`, or `ca-nw` and leave `voice` unset — phoonnx will select the appropriate Matxa dialect variant automatically.

## Other available Matxa variants

| Voice ID | Vocoder | Notes |
|----------|---------|-------|
| `OpenVoiceOS/matxa-cat-multispeaker-vocos-2stage` | alVoCat/Vocos | Recommended — closest to original plugin |
| `OpenVoiceOS/matxa-cat-multispeaker-wavenext-2stage` | WaveNext | Two-stage with WaveNext vocoder |
| `OpenVoiceOS/matxa-cat-multispeaker-wavenext` | WaveNext (baked in) | End-to-end, no separate vocoder |
| `OpenVoiceOS/matxa-cat-multispeaker-hifigan` | HiFi-GAN | End-to-end |
| `OpenVoiceOS/matxa-cat-multiaccent-wavenext` | WaveNext | Multiaccent variant |
| `OpenVoiceOS/matxa-cat-central-graphemes-v2` | — | Grapheme-based, no espeak-ng required |

This plugin was developed by [TigreGotico](https://tigregotico.pt) for OpenVoiceOS under the [ILENIA](https://proyectoilenia.es) project.

Original plugin by the OpenVoiceOS community.
🍵 [Matxa-TTS](https://huggingface.co/projecte-aina/matxa-tts-cat-multiaccent) and 🥑 [alVoCat](https://huggingface.co/projecte-aina/alvocat-vocos-22khz) by Projecte AINA.

![img_1.png](img_1.png)
> 🍵 Matxa-TTS and 🥑 alVoCat were funded by the Generalitat de Catalunya within the framework of [Projecte AINA](https://politiquesdigitals.gencat.cat/ca/economia/catalonia-ai/aina).
