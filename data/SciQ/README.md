# SciQ (Reformatted)

This dataset is derived from the [allenai/sciq](https://huggingface.co/datasets/allenai/sciq) dataset.

## Original Format
The original SciQ dataset provides the following columns:
- `question`
- `distractor3`
- `distractor1`
- `distractor2`
- `correct_answer`
- `support`

Example:

```

question,distractor3,distractor1,distractor2,correct\_answer,support
"Compounds that are capable of accepting electrons, such as o2 or f2, are called what?",residues,antioxidants,Oxygen,oxidants,"Oxidants and Reductants ..."

```

## Reformatted Format
I reformatted the dataset into a **multiple-choice QA format** with the following columns:
- `question`
- `context` (renamed from `support`)
- `A`, `B`, `C`, `D` (answer candidates, shuffled each example)
- `answer` (the correct label: A/B/C/D)

Example:

```

question,context,A,B,C,D,answer
"Compounds that are capable of accepting electrons, such as o2 or f2, are called what?","Oxidants and Reductants ...",residues,Oxygen,oxidants,antioxidants,C

```

## Notes
- The answer choices are **shuffled** per example to avoid positional bias.
- `answer` indicates the **correct option label** after shuffling.
- Only the **test split** was reformatted in this script, but it can be easily adapted for train/validation.