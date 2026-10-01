# Experiment plan

Our main question: can adaptive sampling find more rare positive examples than random sampling, given the same number of LLM labels?

## First baseline

1. Choose a dataset and write down the binary predicate.
2. Make a fixed training pool and held-out test split before sampling. Count positives in each split.
3. Compute embeddings once and record the time and model used.
4. Sample from the training pool, get labels, and fit a class-weighted logistic regression proxy.
5. Evaluate against human gold labels on the held-out split.

Human labels can be used as a simulated labeler while checking the pipeline. Mark those runs clearly; they do not measure LLM label quality or cost. Gold test labels must never guide sampling or training.

If a sample contains only one class, record it as a failed training run. Do not silently add gold positives to make it work.

## Sampling comparison

Start with random sampling, then add uncertainty sampling and a cluster-based adaptive sampler. Give each method the same total label budget, including its initial sample. Use the same splits, embeddings, and seeds.

For the cluster sampler, reserve some budget for exploration so a cluster is not ignored just because its first labels were negative.

## What to record

- Dataset version, predicate, split IDs, positive rate, config, and seed.
- Label source; for LLM runs, model, prompt, cached responses, and actual API calls.
- Positives found per label request and number of distinct positive subcategories where annotations support that measure.
- Precision, recall, F1, and confusion matrix against held-out human labels.
- Embedding, labeling, sampling, training, and inference time separately.
- Token usage and labeling cost for actual LLM runs.

Keep the test set untouched while tuning. If we need to choose a threshold, use a separate validation split.

## Before the final comparison

Finalize at least three datasets covering the categories in the handout. Check label availability and dataset terms before downloading. Freeze dependency versions and record hardware once the baseline works. Repeat runs across seeds and report variation, including failed runs.
