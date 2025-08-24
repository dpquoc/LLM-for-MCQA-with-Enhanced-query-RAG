# OpenBookQA (Reformatted)

This dataset is derived from the [allenai/openbookqa](https://huggingface.co/datasets/allenai/openbookqa) dataset.

## Original Format
The original OpenBookQA dataset provides the following columns:
- `id`
- `question_stem`
- `choices` (dictionary containing arrays of choice texts and labels)
- `answerKey`
- `fact1` (only available in the "additional" subset)
- `humanScore`
- `clarity`
- `turkIdAnonymized`

Example:

```
id,question_stem,choices,answerKey,fact1,humanScore,clarity,turkIdAnonymized
8-343,"A person wants to start saving money so that they can afford a nice vacation at the end of the year. After looking over their budget and expenses, they decide the best way to save money is to","{'text': array(['make more phone calls', 'quit eating lunch out',
       'buy less with monopoly money', 'have lunch with friends'],
      dtype=object), 'label': array(['A', 'B', 'C', 'D'], dtype=object)}",B,,,,
```

## Dataset Composition
OpenBookQA consists of two subsets:
- **Main subset**: Contains questions without additional context (fact1 column is empty)
- **Additional subset**: Contains questions with supporting facts in the fact1 column

Both subsets were combined for the reformatted version.

## Reformatted Format
I reformatted the dataset into a **multiple-choice QA format** with the following columns:
- `question` (renamed from `question_stem`)
- `context` (extracted from `fact1`)
- `A`, `B`, `C`, `D` (answer candidates with preserved label order)
- `answer` (the correct label: A/B/C/D)

Example:

```
question,context,A,B,C,D,answer
"A person wants to start saving money so that they can afford a nice vacation at the end of the year. After looking over their budget and expenses, they decide the best way to save money is to","",make more phone calls,quit eating lunch out,buy less with monopoly money,have lunch with friends,B
```

## Important Notes
- **Context availability**: The `context` column is derived from the `fact1` column, which is **only available in the "additional" subset**. Approximately half of the dataset (the "main" subset) will have **empty context values**.
- **Usage recommendation**: Consider **not relying on the context column** for model training or evaluation, as it's inconsistently available across the dataset.
- **Label preservation**: Unlike some reformatting approaches, the original A/B/C/D labels are preserved in their correct positions to maintain consistency with the original dataset structure.
- **Combined dataset**: Both "main" and "additional" test splits were combined into a single reformatted file.
- Only the **test split** was reformatted in this script, but it can be easily adapted for train/validation splits.