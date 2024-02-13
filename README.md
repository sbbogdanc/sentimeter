# Sentimeter

## Sentiment Analysis Model on Vertex AI with Hugging Face 🤗

This project showcases building and deploying a text sentiment classification model. The model is developed by finetuning [BERT][bert], a popular NLP foundational model from [Hugging Face][hf]. 

To facilitate model development, deployment, and management, the project leverages various services including [Vertex AI][vertex], [Pytorch SDK][pytorch], [Artifact Registry][ar], [Cloud Build][cb], [Cloud Deploy][cd] and [Cloud Storage][cs]. 

## Notebook

You can build and deploy the model on Vertex AI Workbench, which is a Jupyter notebook-based development environment. Start by [creating][vertex-wb] a Vertex AI Workbench instance and [cloning][vertex-wb-git] this GitHub repository in your instance. Then, you can open the [notebook](notebook.ipynb) within your Vertex AI Workbench instance.

## Automation 

### Cloud Build & Cloud Deploy

Coming soon...

### GitHub Actions

Coming soon...

[bert]: https://huggingface.co/bert-base-cased
[hf]: https://huggingface.co/
[vertex]: https://cloud.google.com/vertex-ai
[ar]: https://cloud.google.com/artifact-registry
[cb]: https://cloud.google.com/build
[cd]: https://cloud.google.com/deploy
[cs]: https://cloud.google.com/storage
[pytorch]: https://pytorch.org/
[vertex-wb]: https://cloud.google.com/vertex-ai/docs/workbench/instances/create#consol
[vertex-wb-git]: https://cloud.google.com/vertex-ai/docs/workbench/instances/save-to-github#clone-a-repo
