# What is the difference between open source and open weight models?

The core difference is that open-source models provide full transparency, including training data, code, and weights, while open-weight models only provide the final trained parameters (weights) without disclosing how they were trained. Open weights allow you to run and tune models, but open source allows full auditing and scientific reproduction.

## Open Weight Models (e.g., Llama 3, Mistral, Qwen) [Edge Technology]

- What you get: 
The downloadable, executable weights (parameters) that make the model work.

- What you can do: 
Run on your own infrastructure, fine-tune (adapt to specific tasks), and build applications.

- What is hidden: 
The training code, the dataset, and the specific training process.

- Best for: 
Rapid deployment of powerful models and private, local hosting.

## Open Source Models (e.g., BLOOM, OLMo)

- )What you get: 
Weights plus training code, dataset information, and architecture details.

- What you can do: 
Everything with open-weight, plus full auditing, full retraining, and scientific replication.

- What is shared: 
Total transparency from start to finish.

- Best for: 
Research, education, and applications requiring total transparency and accountability.

## Summary Table of Differences

- Weights: Available in both.

- Training Data/Code: Only in true Open Source.

- Modification: Both allow fine-tuning, but open-source allows architectural changes.

- Transparency: Low/Medium (Weights) vs. High (Source).

Many models commonly called "open-source" are actually "open-weight," as companies often keep the training data secret for competitive or legal reasons.

Refs:

[Master Gemma 4 in 20 Minutes Ali H. Salem ](https://www.youtube.com/watch?v=yJr_kTCOkFo&t=12s)  