# Example for development Spark Jobs with Spark on K8S Operator

## Preparation

1) Install and configure Spark Operator
2) Clone this repository.
3) Apply templates with ServiceAccount, Role and Role Binding:
```console
kubectl apply -f ./templates
```

## Example with configmap

1) Create configmap for application file:
```console
kubectl create configmap demo-spark-job -n default --from-file=pi.py
```
2) Run Spark job
```console
kubectl apply -f spark-with-configmap.yaml
```
3) Check driver logs. You will see the next text:
```console
Pi is roughly 3.147400
```
4) Change some code in the ConfigMap. For example:
Line
```python
print("Pi is roughly %f" % (4.0 * count / n))
```
to line
```python
print("Pi is roughly %f" % (5.0 * count / n))
```
6) Delete your SparkApplication:
```console
kubectl delete -f spark-with-configmap.yaml
```
Then run it again:
```console
kubectl apply -f spark-with-configmap.yaml
```
7) Check driver logs. You will see the next text:
```console
Pi is roughly 3.919250
```

## Example with Git clone init container

1) Fork this repository.
2) Within your fork change repository address in the file spark-with-git-clone.yaml:
Line
```yaml
- https://github.com/jenoOvchi/spark-config-example.git
```
to line
```yaml
- https://github.com/<your-github-name>/spark-config-example.git
```
3) Clone your fork repository.
4) Run Spark job
```console
kubectl apply -f spark-with-git-clone.yaml
```
5) Check driver logs. You will see the next text:
```console
Pi is roughly 3.147400
```
6) Change some code in the file pi.py in your fork repository. For example:
Line
```python
print("Pi is roughly %f" % (4.0 * count / n))
```
to line
```python
print("Pi is roughly %f" % (5.0 * count / n))
```
7) Delete your SparkApplication:
```console
kubectl delete -f spark-with-git-clone.yaml
```
Then run it again:
```console
kubectl apply -f spark-with-git-clone.yaml
```
7) Check driver logs. You will see the next text:
```console
Pi is roughly 3.919250
