# The Sound of Pixels — Paper Summary (ECCV 2018)

Here is a brief summary of the paper **"The Sound of Pixels"** by Hang Zhao and colleagues at MIT and Columbia University, released at ECCV 2018.

The paper presents **PixelPlayer**, a learned model that can disentangle and localize sound in a video — by determining which **pixels are producing which sound** — without ever seeing labeled data.

---


## Introduction

For us in real life, when we see a person playing guitar and another person playing some other instrument, we can simply identify who is playing what by looking and hearing.

But we can't automate it.

The key concept here is:
**Can a machine learn which part of the image is making which sound — without labels?**

---

## PixelPlayer System

PixelPlayer is a system that:
- Given Video and audio as input
- Separates the sound into it's sources (flute and violin for example)
- Determines which parts of the video (pixels) are producing each sound

This allows us to hear different sections of a video independent of each other.

---

## How It Works

PixelPlayer consists of three principal components:

1. **Video analysis network** — extracts visual features for every pixel using a ResNet
2. **Audio analysis network** — applies a U-Net to separate the audio spectrogram into K parts
3. **Audio synthesizer** — blends visual and audio attributes in order to output masks to take out target sound from the spectrogram

Finally, it's the individual, separated audio signal for each picture area.

![Architecture diagram](/img/fig2.jpeg)

---

## Training Method

Training is optimized in that:

- Choose two arbitrary videos (e.g., one trumpet and one violin)
- Combine their audio streams together
- Uses frames from each video to help the model in separating the sounds

The model learns task to separate sounds  *based on visual information*, and it doesn't require labels, which is a form of **self-supervised learning**.

![Mix-and-Separate pipeline](/img/fig3.jpeg)

---

## MUSIC Dataset

To train PixelPlayer, the authors collected a new dataset called **MUSIC** (Multimodal Sources of Instrument Combinations):

- 714 videos from YouTube
- 11 musical instruments
- Includes both solos and duets

The dataset includes instruments such as flute, violin, cello, guitar, trumpet, and so on.

![Category distribution and sample frames](/img/fig4.jpeg)
![Category distribution and sample frames](/img/fig5.jpeg)

---

## Results

- The model performs well in the aspect of sound separation and localization
- Best performance results is observed while applying **binary masks** and **log-scale spectrograms**
- And also this audio-only baselines such as NMF and DeepConvSep

The model also learns to focus on certain channels for various instruments. For example, one channel may respond only to violins, another channel to guitars.

![Spectrogram outputs before and after separation](/img/fig6.jpeg)
![Heatmaps showing pixel-level sound energy](/img/fig7.jpeg)
![Sound clustering](/img/fig8.jpeg)
![Confusion matrices for instrument detection](/img/fig9.jpeg)
![Channel-specific activations](/img/fig10.jpeg)

---

## Human Evaluation

The authors also tried the model on actual humans at Amazon Mechanical Turk:

1. **Sound separation** — They asked individuals what instrument they listened to. The binary mask model was most accurate.
2. **Visual-sound matching** — They asked individuals: "Is the sound originating from this pixel?" The model performed here too.

This indicates the model isn't just theory — individuals actually notice the difference.

---

## Applications

Some of the awesome things this system can do:

- Control the volume of a particular instrument in a video
- Erase background or extract a sound source
- Recognize which object is producing sound in video scenes

This finds application in video editing, accessibility, smart audio mixing, and beyond.

---

## YouTube Explanation Video

I also created a brief explanation video for this paper. You can view it here:

**[Watch the explanation video on YouTube](https://youtu.be/yKmhQB4742M)**

---

## Conclusion

- PixelPlayer connects sound with vision without manual tags
- It disentangles and localizes the sounds in video via self-supervised learning
- It demonstrates robust results on the MUSIC dataset and performs well even for humans

This paper provides new direction on how sound and vision can complement each other in AI.

---

## Project Link

Original project page:
[http://sound-of-pixels.csail.mit.edu](http://sound-of-pixels.csail.mit.edu)

---

## Citation

```bibtex
@inproceedings{zhao2018sound,
  title={The Sound of Pixels},
author={Zhao, Hang and Gan, Chuang and Rouditchenko, Andrew and Vondrick, Carl and McDermott, Josh and Torralba, Antonio},
  booktitle={ECCV},
  year={2018}
