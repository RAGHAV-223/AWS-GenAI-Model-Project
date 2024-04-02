# AWS-GenAI-Model-Project
### LLM Model Evaluation File
In this notebook, we deploy the Meta Llama 2 7B model and evaluate it's text generation capabilities and domain knowledge. We used the SageMaker Python SDK for Foundation Models and deploy the model for inference. 

The Llama 2 7B Foundation model performs the task of text generation. It takes a text string as input and predicts next words in the sequence.
#### Set Up
---
!pip install ipywidgets==7.0.0 --quiet
!pip install --upgrade sagemaker datasets --quiet
---
There are some initial steps required for setup. If you recieve warnings after running this cells, you can ignore them as they won't impact the code running in the notebook. Restart the Kernel after you run this cell.

To deploy the model on Amazon Sagemaker, you need to setup and authenticate the use of AWS services. Validate your role is the Sagemaker IAM role you created for the project by running the next cell.

After role varfication deploy the texxt generation model : Meta Llama 2 7B

---
from sagemaker.jumpstart.model import JumpStartModel

model = JumpStartModel(model_id=model_id, model_version=model_version, instance_type="ml.g5.2xlarge")
predictor = model.deploy()
---
This Python code is used to deploy a machine learning model using Amazon SageMaker's JumpStart library. 

1. Import the JumpStartModel class from the sagemaker.jumpstart.model module.

2. Create an instance of the JumpStartModel class using the model_id and model_version variables created in the previous cell. This object represents the machine learning model you want to deploy.

3. Call the deploy method on the JumpStartModel instance. This method deploys the model on Amazon SageMaker and returns a Predictor object.

The Predictor object (predictor) can be used to make predictions with the deployed model. The deploy method will automatically choose an endpoint name, instance type, and other deployment parameters. If you want to specify these parameters, you can pass them as arguments to the deploy method.
You might see a warning "For forward compatibility, pin to model_version..." You can ignore this warning, just wait for the model to deploy.

#### Invoke the endpoint, query and parse response
The model takes a text string as input and predicts next words in the sequence, the input we send it is the prompt. 

*After you've test the model, run the cells below to delete the model deployment* 

IF YOU FAIL TO RUN THE CELLS BELOW YOU WILL RUN OUT OF BUDGET TO COMPLETE THE PROJECT
Verify your model endpoint was deleted by visiting endpoints under 'Inference' in the left navigation menu of the Sagemaker dashboard.
### Model Fine-tuning File
In this notebook, we'll fine-tune the Meta Llama 2 7B large language model, deploy the fine-tuned model, and test it's text generation and domain knowledge capabilities. 

Fine-tuning refers to the process of taking a pre-trained language model and retraining it for a different but related task using specific data. This approach is also known as transfer learning, which involves transferring the knowledge learned from one task to another. Large language models (LLMs) like Llama 2 7B are trained on massive amounts of unlabeled data and can be fine-tuned on domain datasets, making the model perform better on that specific domain.

#### Set up


Install and import the necessary packages. Restart the kernel after executing the cell below. 
---
!pip install --upgrade sagemaker datasets
---

Selecting the model to fine-tune: we will choose the same model as in Evaluation file ( Meta Llama 2 7B) to compare the outputs.

Next we choose the training dataset text for the domain ,here, we choose an IT domain expert model
  
#### Deploy the fine-tuned model
After tunning we deploy the model. We will compare the performance of the fine-tuned and pre-trained model.

#### Evaluate the pre-trained and fine-tuned model
Use the same input from the model evaluation step to evaluate the performance of the fine-tuned model and compare it with the base pre-trained model. Run the same prompts on the fine-tuned model to evaluate it's domain knowledge.   

Do the outputs from the fine-tuned model provide domain-specific insightful and relevant content? You can continue experimenting with the inputs of the model to test it's domain knowledge. 


*After you've test the model, run the cells below to delete the model deployment* 
---
finetuned_predictor.delete_model()
finetuned_predictor.delete_endpoint()
---
IF YOU FAIL TO RUN THE CELLS BELOW YOU WILL RUN OUT OF BUDGET TO COMPLETE THE PROJECT
