## Deployment

Deploying a PyTorch [model on Vertex AI](https://cloud.google.com/vertex-ai/docs/predictions/getting-predictions) requires a custom container that serves online predictions on a Vertex AI Endpoint. Deploy a container running [PyTorch's TorchServe](https://pytorch.org/serve/) tool in order to serve predictions from the fine-tuned transformer model for a sentiment analysis task. Then, use Vertex AI's online prediction service to classify the sentiment of input texts. 

### Deploying a model on Vertex AI using a custom container

To use a custom container to serve predictions from a PyTorch model, you must provide Vertex AI with a Docker container image that runs an HTTP server application, such as TorchServe in this case. Learn more about the [prediction container requirements on Vertex AI](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements). In summary, the following steps are needed to deploy a PyTorch model on Vertex AI:

1. Package the trained model artifacts including [default](https://pytorch.org/serve/#default-handlers) or [custom](https://pytorch.org/serve/custom_service.html) handlers by creating an archive file using [Torch model archiver](https://github.com/pytorch/serve/tree/master/model-archiver).
2. Build a [custom container](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements) compatible with Vertex AI to serve the model using TorchServe.
3. Upload the model with the custom container image to serve predictions as a Vertex AI model resource.
4. Create a Vertex AI Endpoint and [deploy the model](https://cloud.google.com/vertex-ai/docs/predictions/deploy-model-api) resource.

#### Custom model handler to handle prediction requests

When passing input text to the fine-tuned transformer model, the input text needs to be pre-processed. Once the model generates predictions, some post-processing has to be performed on the generated output to label it into the underlying classes and serve their probabilities or confidence scores. 

To include the steps like pre-processing and post-processing, create a custom handler script that is packaged with the model artifacts. Later, TorchServe executes the script when deployed. 

Custom handler script in `predictor/custom_handler.py` does the following:
* Pre-process input text before sending it to the model for inference.
* Customize how the model is invoked for inference.
* Post-process output from the model before sending back a response.

For the custom handler, the `index_to_name.json` mapping file  is used to associate the target labels with their meaningful names while formatting the prediction responses.

Learn more about defining a custom handler from [TorchServe documentation](https://pytorch.org/serve/custom_service.html).