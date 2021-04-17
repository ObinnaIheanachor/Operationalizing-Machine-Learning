# Operationalizing-Machine-Learning

This is an end-to-end machine learning project on Microsoft Azure where I have configured a cloud-based machine learning production model, deployed, and consumed it. Using the <a href='https://archive.ics.uci.edu/ml/datasets/Bank+Marketing'>Bank Marketing Dataset</a>, I trained a machine learning model leveraging the AutoML feature of Azure Machine Learning Studio, deployed it into production using Azure Container Instance (ACI) and consumed it using REST endpoints. I also created, published and consumed a pipeline to automate the whole process.

## Architectural Diagram
![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/architecture.png)

The architectural diagram above shows the flow of operations from start to finish. Let's understand each step:
* Register the Dataset: This involves uploading the dataset into Azure Machine Learning Studio. This can be done using the URL or uploading directly from a local folder.
* AutoML run: Here we set up configurations like compute cluster, type of machine learning task (in this case classification), exit criterion, etc. This trains different models on our uploaded dataset.
* Deploy the best model: Here we select the best performing model from our AutoML run and deploy into production using `Azure Container Instance (ACI)` or `Azure Kubernetes Service (AKS)`.
* Enable logging and Application Insights: This can be done either when deploying the model into production from the studio or afterwards using a python script. This helps us keep track of deployed model performance and number of successful/failed requests.
* Consume Model Endpoints: After deploying the model, a REST endpoint is generated and this enables other services to interact with our deployed model. We can send requests to the deployed model  and get responses (predictions).
* Create and Publish a Pipeline: Using the Azure Python SDK with the aid of a Jupyter Notebook, we can create and publish a pipeline. This requires a `config.json` file to be present in the working directory. Using pipelines, we can automate the whole process of training and deploying our model.
### Future Work
This project can be improved on by:
* Use a parallel run step in the pipeline
* Test a local container with a downloaded model
* Using pipelines to automate the whole workflow from data preparation, to machine learning tasks and deployment.
* Using the Apache Benchmark tool to set a measure of optimal performance.

## Key Steps
1. **Authentication**: This was done automatically in the course Workspace. When working on your own Azure account,  you will need to install the Azure Machine Learning Extension which allows you to interact with Azure Machine Learning Studio, part of the az command. After having the Azure machine Learning Extension, you will create a Service Principal account and associate it with your specific workspace.

2. **Automated ML Experiment**: In this step an AutoML run was configured and several models were trained on the <a href='https://archive.ics.uci.edu/ml/datasets/Bank+Marketing'>Bank Marketing Dataset</a>. This involves configuring a compute cluster, type of machine learning task etc. From our run, the best performing model is `voting ensemble` as shown below.

**Registered Dataset**

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/1.%20dataset.PNG)

**Experiment Completed**

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/2.%20experiment%20completed.PNG)

**Best Model**

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/3.%20best%20model.PNG)



3. **Deploy Best Model and Enable Logging**: The best model from our AutoML run is deployed into production using `Azure Container Instance (ACI)` and we can access endpoints through which other services can interact with our deployed model.
We also enable authentication during deployment so keys are generated which other services can use to authenticate before interacting with our deployed model.

After deploying our best model, we can enable Application Insights and retrieve logs (this can also be done during deployment).

**Model Deployed and Application Insights Enabled**

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/application%20insights%20enabled.PNG)



4. **Swagger Documentation**: [Swagger](https://swagger.io/blog/api-development/getting-started-with-swagger-i-what-is-swagger/) is a tool for building, and documenting REST APIs. It can be used to share documentation among product managers, testers, and developers and can also be used by various tools to automate API-related processes.

Azure provides a swagger.json URL that can be used to create a web site that documents the HTTP endpoint for a deployed model. Here we consumed our deployed model using swagger and displayed the contents of the API for the model as shown below;

**Swagger Output**

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/swagger%201.PNG)

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/swagger%202.PNG)

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/swagger%203.PNG)

5. **Consume Model Endpoint**: Once the model is deployed, we use the python script [endpoint.py](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/endpoint.py) provided to interact with the trained model and return an output (prediction) as shown below;

**Endpoint.py output**

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/endpoint.py%20output.PNG)

6. **Create, Publish, and Consume a Pipeline**: Here we use the Azure Python SDK with the aid of Jupyter Notebook to create, publish, and consume a pipeline as shown below;

**Published Pipeline**

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/pipeline%20is%20running.PNG)

**Pipeline Endpoint**

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/pipeline%20endpoint.PNG)

**Running Pipeline**

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/pipeline%20dataset.PNG)

**Status Active**

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/pipeline%20endpoint2.PNG)

**Run Widget**

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/run%20details.PNG)

**Run Completed**

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/pipeline%20run%20completed.PNG)

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/run%20finished.PNG)


## Screen Recording
This [video](https://youtu.be/yeOZCbPX2-o) shows the entire process of the working ML application.

## Standout Suggestions

`Apache Benchmark` is an easy and popular tool for benchmarking HTTP services. I benchmarked the endpoint created from the deployed model using Apache bench tool. This helps to create a baseline or acceptable performance measure. Benchmarking HTTP APIs is used to find the average response time for a deployed model.

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/benchmark%20pic.PNG)

![](https://github.com/ObinnaIheanachor/Operationalizing-Machine-Learning/blob/master/Screenshots/benchmark%202.PNG)
