## Introduction
Whisper is a pre-trained model for automatic speech recognition (ASR) published in September 2022 by the authors Alec Radford et al. from OpenAI. Unlike many of its predecessors, such as Wav2Vec 2.0, which are pre-trained on un-labelled audio data, Whisper is pre-trained on a vast quantity of labelled audio-transcription data, 680,000 hours to be precise. This is an order of magnitude more data than the un-labelled audio data used to train Wav2Vec 2.0 (60,000 hours). What is more, 117,000 hours of this pre-training data is multilingual ASR data. This results in checkpoints that can be applied to over 96 languages, many of which are considered low-resource.

This quantity of labelled data enables Whisper to be pre-trained directly on the supervised task of speech recognition, learning a speech-to-text mapping from the labelled audio-transcription pre-training data 
1
1
 . As a consequence, Whisper requires little additional fine-tuning to yield a performant ASR model. This is in contrast to Wav2Vec 2.0, which is pre-trained on the unsupervised task of masked prediction. Here, the model is trained to learn an intermediate mapping from speech to hidden states from un-labelled audio only data. While unsupervised pre-training yields high-quality representations of speech, it does not learn a speech-to-text mapping. This mapping is only learned during fine-tuning, thus requiring more fine-tuning to yield competitive performance.

When scaled to 680,000 hours of labelled pre-training data, Whisper models demonstrate a strong ability to generalise to many datasets and domains. The pre-trained checkpoints achieve competitive results to state-of-the-art ASR systems, with near 3% word error rate (WER) on the test-clean subset of LibriSpeech ASR and a new state-of-the-art on TED-LIUM with 4.7% WER (c.f. Table 8 of the Whisper paper). The extensive multilingual ASR knowledge acquired by Whisper during pre-training can be leveraged for other low-resource languages; through fine-tuning, the pre-trained checkpoints can be adapted for specific datasets and languages to further improve upon these results.

Whisper is a Transformer based encoder-decoder model, also referred to as a sequence-to-sequence model. It maps a sequence of audio spectrogram features to a sequence of text tokens. First, the raw audio inputs are converted to a log-Mel spectrogram by action of the feature extractor. The Transformer encoder then encodes the spectrogram to form a sequence of encoder hidden states. Finally, the decoder autoregressively predicts text tokens, conditional on both the previous tokens and the encoder hidden states. Figure 1 summarises the Whisper model.
## get the data
to get the data you can load it from this link https://zenodo.org/record/5482551/accessrequest
## Prepare Environment
We'll employ several popular Python packages to fine-tune the Whisper model. We'll use datasets to download and prepare our training data and transformers to load and train our Whisper model. We'll also require the soundfile package to pre-process audio files, evaluate and jiwer to assess the performance of our model. Finally, we'll use gradio to build a flashy demo of our fine-tuned model.

```shell
!pip install datasets>=2.6.1
!pip install git+https://github.com/huggingface/transformers
!pip install librosa
!pip install evaluate>=0.30
!pip install jiwer
!pip install gradio


