# ToneCheck

**Can a computer hear Mandarin tones, and where does it get them wrong?**

> Status: in progress. No results yet. Every table below is a placeholder that will be filled in as experiments finish.

## The idea

In Mandarin, the same syllable means different things depending on its pitch pattern. *mā* (mother), *má* (hemp), *mǎ* (horse) and *mà* (to scold) differ only in tone. Learners find tones hard, and getting feedback usually needs a teacher listening in real time.

This project asks how well different kinds of models can recognize tones from audio, and, more interesting, what kinds of mistakes they make.

## Questions

1. How well does a simple model that only looks at pitch recognize tones?
2. Do speech models that learn from raw audio do better, and do they already "know" tone before we train them on it?
3. Where do models fail? Likely suspects: the neutral tone, tones 2 versus 3, and the way third tones change before other third tones (tone sandhi).
4. What happens when the speaker is a learner instead of a native speaker?

## How it works

1. **Data.** About 85 hours of read speech from 218 native speakers (AISHELL-3), with the intended tones of every syllable written down.
2. **Cutting speech into syllables.** A forced aligner finds where each syllable starts and ends.
3. **Three approaches, from simple to heavy:**
   - *Pitch only:* measure the pitch curve of each syllable and classify it with a basic model.
   - *Listening only:* take what a pretrained speech model already represents about the audio and see whether tone can be read off it.
   - *Fine-tuned:* train the speech model directly on tone labels.
4. **Fair testing.** Speakers in the test set never appear in training, so scores reflect new voices and not memorized ones.
5. **Learner test.** A small set of recordings from Mandarin learners, used only for testing, to measure how much performance drops when the speaker isn't a native.

## Results

### Native speakers (held-out speakers)

| Approach | Accuracy | Notes |
|---|---|---|
| Pitch only | n/a | to do |
| Pretrained speech model, frozen | n/a | to do |
| Pretrained speech model, fine-tuned | n/a | to do |

### Native versus learner speech

| Approach | Native accuracy | Learner accuracy | Drop |
|---|---|---|---|
| Pitch only | n/a | n/a | n/a |
| Fine-tuned | n/a | n/a | n/a |

### Where the models go wrong

To do: confusion matrix, accuracy by tone, accuracy on sandhi and neutral-tone syllables, with audio examples of failures.

## Limitations (known in advance)

- The learner set will be small and collected by me, so its conclusions are suggestive and not definitive.
- Learner recordings and the training corpus differ in microphone and room, so part of any "learner gap" may be recording conditions.
- The tone labels describe what a speaker was supposed to say. For learners, what they actually said may differ, so labels there need a native listener's check.
- This is a study of tone recognition, not a pronunciation grader.

## Roadmap

1. Get the data, align it, and plot the average pitch curve for each tone.
2. Pitch-only baseline.
3. Speech-model probing and fine-tuning.
4. Learner recordings and the native-versus-learner comparison.
5. Error analysis and write-up.
6. Later: reuse the best model inside the Hanyu Mandarin-learning bot as a pronunciation check.

## Reproducing

Needs Linux, `uv`, `make`, and about 40 GB of free disk.

```
make setup      # install dependencies
make download   # fetch the corpus
make extract    # unpack it
```

Later stages will be added here as they are built.

## Data and credits

Speech data: [AISHELL-3](https://www.openslr.org/93/), published by Beijing Shell Shell Technology Co., Ltd. Check the license on the dataset page before reuse. Code license: to be added.
