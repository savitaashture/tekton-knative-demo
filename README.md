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
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/master/task/git-clone/0.2/git-clone.yaml
```
3 . Install `buildah` task
```yaml
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/master/task/buildah/0.2/buildah.yaml
```
4 . Install `kn` task
```yaml
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/master/task/kn/0.1/kn.yaml
```

## Install Tekton TaskRun
1 . Create PVC
```yaml
kubectl apply -f common/pvc.yaml
```

2 . TaskRun for `git-clone`
```yaml
kubectl apply -f TaskRuns/git-clone.yaml
```

3 . TaskRun for `buildah`
```yaml
kubectl apply -f TaskRuns/buildah.yaml
```

4 . TaskRun for `kn`
```yaml
kubectl apply -f TaskRuns/kn.yaml
```

## Install Tekton Pipeline

```yaml
kubectl apply -f pipeline/pipeline.yaml
```

## Install Tekton PipelineRun

* Create PVC
```yaml
kubectl apply -f common/pipeline-pvc.yaml
```
* Create PipelineRun
```yaml
kubectl apply -f pipeline/pipelinerun.yaml
```

```text
kubectl create secret docker-registry container-registry --docker-server=quay.io/savitaashture --docker-username=savitaashture --docker-password=12_abcdefG -n demo
```