# mlflow-colab

This repo tries to use [mlfow](https://mlflow.org/) in google colab. MLflow is an open source platform to manage the ML lifecycle. It provides tools to conduct experiments, manage models for reproducibility, as well as [mlflow ui](https://www.mlflow.org/docs/latest/tracking.html) for logging, and visualization. 


## notebook
[MLflow](./MLflow.ipynb) contains all the codes for executing [irs classification](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.load_iris.html) problem using `discision tree`, `logistic regression`, and `SVM`, as well as the `mlflow` setting up. 
```python
mlflow.set_experiment('Iris Classification')
...
mlflow.log_param('dataset', 'iris')
...
mlflow.log_artifact(model_file_name)
mlflow.log_artifact(confusion_matrix_file_name)
...
mlflow.log_metric('accuracy', acc)
```

After executing this notebook, the folder will look like:

	mlfow
	├── mlruns
	│   └── 0
	│       ├── 09adde98fdc346e98cffd3302597bed0
	│       │    ├── artifacts
	│       │    │    ├── decision_tree.pkl
	│       │    │    ├── decision_tree_confusion_matrix.png
	│       │    │    ├── logistric_regression.pkl
	│       │    │    ├── logistric_regression_confusion_matrix.png
	│       │    │    ├── svm.pkl
	│       │    │    └── svm_confusion_matrix.png
	│       │    ├── metrics
	│       │    │   └── accuracy
	│       │    ├── params
	│       │    │   ├── dataset
	│       │    │   └── model_name
	│       │    ├── tags
	│       │    │   ├── mlflow.source.name
	│       │    │   ├── mlflow.source.type
	│       │    │   └── mlflow.user
	│       │    └── meta.yaml
	│       │
	│       └── meta.yaml
	└── util.py

## mlflow UI
there is no direct link from mlfow ui to google colab/drive yet. I used pyngrok to route. learnt from https://github.com/mlflow/mlflow/issues/2350

```python
get_ipython().system_raw("mlflow ui --port 5000 &")
public_url = ngrok.connect(port="5000", proto="http", options={"bind_tls": True})
```



