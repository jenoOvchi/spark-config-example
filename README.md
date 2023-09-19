# spark-config-example

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
