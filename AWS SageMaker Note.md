# AWS SageMaker Notes

## General Architecture

* Two types of API, high level and low level
  * High level API is a simple wrapper for low level API. It handles model creation, deployment, endpoint configuration etc.
  * Low level API consists of a decent chunk of boilerplate code to set up the model, endpoint etc. It provides users with more customization.
* Pricing model is pay by usage. See the price model [here](https://aws.amazon.com/sagemaker/pricing/)
  * Notebook instances
  * Training computing resources
  * Model hosting instances
  * Storage cost

## High Level Observation

* Overall, the training process, deployment and serving is easy to set up assuming we have a prebuilt image/model to use. It will be interesting to see the effort of building a customized ML model using SageMaker.
* It will be tough to compete with SageMaker in terms of ML service offering such as data exploring, training and deployment, especially when customers already have their data stored in S3.
* ETL and data integration are areas that deserve more attentions. Preparing training data and consolidating data from different sources itself is a challenging task. AWS Glue is a solution to this problem, but I am not sure how good it is. And whether Sumo has any competitive advantage in this space.

## Potential Pitfalls

* SageMaker Instance needs to be in the same region as the S3 bucket where the training data is stored.
* The error messages could be obscure without giving much useful debugging information. An example is like the below message where I accidentally reused the same job name for the training process.

``` python
ResourceInUse                             Traceback (most recent call last)
<timed exec> in <module>()

~/anaconda3/envs/python3/lib/python3.6/site-packages/botocore/client.py in _api_call(self, *args, **kwargs)
    315                     "%s() only accepts keyword arguments." % py_operation_name)
    316             # The "self" in this scope is referring to the BaseClient.
--> 317             return self._make_api_call(operation_name, kwargs)
    318
    319         _api_call.__name__ = str(py_operation_name)

~/anaconda3/envs/python3/lib/python3.6/site-packages/botocore/client.py in _make_api_call(self, operation_name, api_params)
    613             error_code = parsed_response.get("Error", {}).get("Code")
    614             error_class = self.exceptions.from_code(error_code)
--> 615             raise error_class(parsed_response, operation_name)
    616         else:
    617             return parsed_response

ResourceInUse: An error occurred (ResourceInUse) when calling the CreateTrainingJob operation:
```

* For a long running training process, Jupyter notebook single thread cell evaluation model is really limiting.
* The training related logging are stored in CloudWatch under **/aws/sagemaker/TrainingJobs** log group. However the logging is not well formatted. The logging info is model dependent.
