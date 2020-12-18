# tekton-knative-demo

## Pre-requisites:
* Cluster should have running [Knative](https://knative.dev/docs/install/any-kubernetes-cluster/#installing-the-serving-component).
* Cluster should have running [Tekton Piepline](https://github.com/tektoncd/pipeline/blob/master/docs/install.md).

## Install Tekton Tasks
1 . Create namespace `demo`
```yaml
kubectl create ns demo
```
2 . Install `git-clone` task
```yaml
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/master/task/git-clone/0.2/git-clone.yaml -n demo
```
3 . Install `buildah` task
```yaml
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/master/task/buildah/0.2/buildah.yaml -n demo
```
4 . Install `kn` task
```yaml
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/master/task/kn/0.1/kn.yaml -n demo
```

## Install Tekton TaskRun
1 . Create PVC
```yaml
kubectl apply -f common/pvc.yaml -n demo
```

2 . TaskRun for `git-clone`
```yaml
kubectl apply -f TaskRuns/git-clone.yaml -n demo
```

3 . TaskRun for `buildah`
```yaml
kubectl apply -f TaskRuns/buildah.yaml -n demo
```

4 . TaskRun for `kn`
```yaml
kubectl apply -f TaskRuns/kn.yaml -n demo
```

## Install Tekton Pipeline

```yaml
kubectl apply -f pipeline/pipeline.yaml -n demo
```

## Install Tekton PipelineRun

* Create PVC
```yaml
kubectl apply -f common/pipeline-pvc.yaml -n demo
```
* Create PipelineRun
```yaml
kubectl apply -f pipeline/pipelinerun.yaml -n demo
```

```text
kubectl create secret docker-registry container-registry --docker-server=<dockerhub> --docker-username=<username> --docker-password=<password> -n demo
```
