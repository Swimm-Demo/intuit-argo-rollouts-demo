---
title: Getting Started with Rollout Details
---
# Getting Started with Rollout Details

This document provides a comprehensive guide to understanding the details of a rollout in the Argo Rollouts framework. It covers various aspects such as metadata, strategy, status, container information, and replica information.

## Rollout Metadata

The <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="20:2:2" line-data="func NewRolloutInfo(">`NewRolloutInfo`</SwmToken> function initializes the <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="27:5:5" line-data=") *rollout.RolloutInfo {">`RolloutInfo`</SwmToken> object with essential metadata. This includes the rollout's name, namespace, labels, annotations, UID, and creation timestamp. This metadata is crucial for identifying and managing the rollout.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/info/rollout_info.go" line="20">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="20:2:2" line-data="func NewRolloutInfo(">`NewRolloutInfo`</SwmToken> function initializes the <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="27:5:5" line-data=") *rollout.RolloutInfo {">`RolloutInfo`</SwmToken> object with metadata such as name, namespace, labels, annotations, UID, and creation timestamp.

```go
func NewRolloutInfo(
	ro *v1alpha1.Rollout,
	allReplicaSets []*appsv1.ReplicaSet,
	allPods []*corev1.Pod,
	allExperiments []*v1alpha1.Experiment,
	allARs []*v1alpha1.AnalysisRun,
	workloadRef *appsv1.Deployment,
) *rollout.RolloutInfo {

	roInfo := rollout.RolloutInfo{
		ObjectMeta: &v1.ObjectMeta{
			Name:              ro.Name,
			Namespace:         ro.Namespace,
			Labels:            ro.Labels,
			Annotations:       ro.Annotations,
			UID:               ro.UID,
			CreationTimestamp: ro.CreationTimestamp,
			ResourceVersion:   ro.ObjectMeta.ResourceVersion,
		},
```

---

</SwmSnippet>

## Rollout Strategy

The rollout strategy, whether Canary or <SwmToken path="pkg/apis/rollouts/v1alpha1/types.go" pos="947:1:1" line-data="	BlueGreen BlueGreenStatus `json:&quot;blueGreen,omitempty&quot; protobuf:&quot;bytes,16,opt,name=blueGreen&quot;`">`BlueGreen`</SwmToken>, is identified and set in the <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="27:5:5" line-data=") *rollout.RolloutInfo {">`RolloutInfo`</SwmToken> object. For Canary strategies, it includes details such as the current step and weight information.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/info/rollout_info.go" line="45">

---

The function identifies the rollout strategy (Canary or <SwmToken path="pkg/apis/rollouts/v1alpha1/types.go" pos="947:1:1" line-data="	BlueGreen BlueGreenStatus `json:&quot;blueGreen,omitempty&quot; protobuf:&quot;bytes,16,opt,name=blueGreen&quot;`">`BlueGreen`</SwmToken>) and sets the relevant details such as the current step and weight information for Canary strategies.

```go
	if ro.Spec.Strategy.Canary != nil {
		roInfo.Strategy = "Canary"
		if ro.Status.CurrentStepIndex != nil && len(ro.Spec.Strategy.Canary.Steps) > 0 {
			roInfo.Step = fmt.Sprintf("%d/%d", *ro.Status.CurrentStepIndex, len(ro.Spec.Strategy.Canary.Steps))
			var steps []*v1alpha1.CanaryStep
			for i := range ro.Spec.Strategy.Canary.Steps {
				steps = append(steps, &ro.Spec.Strategy.Canary.Steps[i])
			}
			roInfo.Steps = steps
		}
		// NOTE that this is desired weight, not the actual current weight
		roInfo.SetWeight = strconv.Itoa(int(replicasetutil.GetCurrentSetWeight(ro)))

		roInfo.ActualWeight = "0"
		currentStep, _ := replicasetutil.GetCurrentCanaryStep(ro)

		if currentStep == nil {
			roInfo.ActualWeight = fmt.Sprintf("%d", weightutil.MaxTrafficWeight(ro))
		} else if ro.Status.AvailableReplicas > 0 {
			if ro.Spec.Strategy.Canary.TrafficRouting == nil {
				for _, rs := range roInfo.ReplicaSets {
```

---

</SwmSnippet>

## Rollout Status

The status of the rollout, including its phase, message, and icon representation, is determined and set in the <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="27:5:5" line-data=") *rollout.RolloutInfo {">`RolloutInfo`</SwmToken> object. This helps in understanding the current state of the rollout.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/info/rollout_info.go" line="81">

---

The status of the rollout, including its phase, message, and icon representation, is determined and set in the <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="27:5:5" line-data=") *rollout.RolloutInfo {">`RolloutInfo`</SwmToken> object.

```go
	phase, message := rolloututil.GetRolloutPhase(ro)
	roInfo.Status = string(phase)
	roInfo.Message = message
	roInfo.Icon = rolloutIcon(roInfo.Status)
```

---

</SwmSnippet>

## Container Information

Information about the containers and their images, both regular and init containers, is added to the <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="27:5:5" line-data=") *rollout.RolloutInfo {">`RolloutInfo`</SwmToken> object. This includes details about the container names and images.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/info/rollout_info.go" line="85">

---

Information about the containers and their images, both regular and init containers, is added to the <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="27:5:5" line-data=") *rollout.RolloutInfo {">`RolloutInfo`</SwmToken> object.

```go
	roInfo.Containers = []*rollout.ContainerInfo{}

	var containerList []corev1.Container
	var initContainerList []corev1.Container
	if workloadRef != nil {
		containerList = workloadRef.Spec.Template.Spec.Containers
		initContainerList = workloadRef.Spec.Template.Spec.InitContainers
	} else {
		containerList = ro.Spec.Template.Spec.Containers
		initContainerList = ro.Spec.Template.Spec.InitContainers
	}

	for _, c := range containerList {
		roInfo.Containers = append(roInfo.Containers, &rollout.ContainerInfo{Name: c.Name, Image: c.Image})
	}

	for _, c := range initContainerList {
		roInfo.InitContainers = append(roInfo.InitContainers, &rollout.ContainerInfo{Name: c.Name, Image: c.Image})
	}
```

---

</SwmSnippet>

## Replica Information

The <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="27:5:5" line-data=") *rollout.RolloutInfo {">`RolloutInfo`</SwmToken> object tracks the number of desired, ready, current, updated, and available replicas. This information is crucial for understanding the deployment status and scaling requirements.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/info/rollout_info.go" line="111">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="27:5:5" line-data=") *rollout.RolloutInfo {">`RolloutInfo`</SwmToken> object tracks the number of desired, ready, current, updated, and available replicas.

```go
	roInfo.Generation = ro.Status.ObservedGeneration

	roInfo.Desired = defaults.GetReplicasOrDefault(ro.Spec.Replicas)
	roInfo.Ready = ro.Status.ReadyReplicas
	roInfo.Current = ro.Status.Replicas
	roInfo.Updated = ro.Status.UpdatedReplicas
	roInfo.Available = ro.Status.AvailableReplicas
	return &roInfo
```

---

</SwmSnippet>

## Main Functions

There are several main functions in this folder. Some of them are <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="20:2:2" line-data="func NewRolloutInfo(">`NewRolloutInfo`</SwmToken>, <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="141:2:2" line-data="// Images returns a list of images that are currently running along with informational tags about">`Images`</SwmToken>, and <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="220:2:2" line-data="func Revisions(r *rollout.RolloutInfo) []int {">`Revisions`</SwmToken>. We will dive a little into <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="20:2:2" line-data="func NewRolloutInfo(">`NewRolloutInfo`</SwmToken> and <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="141:2:2" line-data="// Images returns a list of images that are currently running along with informational tags about">`Images`</SwmToken>.

### <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="20:2:2" line-data="func NewRolloutInfo(">`NewRolloutInfo`</SwmToken>

The <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="20:2:2" line-data="func NewRolloutInfo(">`NewRolloutInfo`</SwmToken> function initializes a new <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="27:5:5" line-data=") *rollout.RolloutInfo {">`RolloutInfo`</SwmToken> object with detailed information about a specific rollout, including metadata, strategy, status, and associated resources.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/info/rollout_info.go" line="20">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="20:2:2" line-data="func NewRolloutInfo(">`NewRolloutInfo`</SwmToken> function initializes a new <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="27:5:5" line-data=") *rollout.RolloutInfo {">`RolloutInfo`</SwmToken> object with detailed information about a specific rollout, including metadata, strategy, status, and associated resources.

```go
func NewRolloutInfo(
	ro *v1alpha1.Rollout,
	allReplicaSets []*appsv1.ReplicaSet,
	allPods []*corev1.Pod,
	allExperiments []*v1alpha1.Experiment,
	allARs []*v1alpha1.AnalysisRun,
	workloadRef *appsv1.Deployment,
) *rollout.RolloutInfo {

	roInfo := rollout.RolloutInfo{
		ObjectMeta: &v1.ObjectMeta{
			Name:              ro.Name,
			Namespace:         ro.Namespace,
			Labels:            ro.Labels,
			Annotations:       ro.Annotations,
			UID:               ro.UID,
			CreationTimestamp: ro.CreationTimestamp,
			ResourceVersion:   ro.ObjectMeta.ResourceVersion,
		},
	}
```

---

</SwmSnippet>

### Images

The <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="141:2:2" line-data="// Images returns a list of images that are currently running along with informational tags about">`Images`</SwmToken> function returns a list of images that are currently running along with informational tags about which stack they belong to and which experiment template they are part of.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/info/rollout_info.go" line="141">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="141:2:2" line-data="// Images returns a list of images that are currently running along with informational tags about">`Images`</SwmToken> function returns a list of images that are currently running along with informational tags about which stack they belong to and which experiment template they are part of.

```go
// Images returns a list of images that are currently running along with informational tags about
// 1. which stack they belong to (canary, stable, active, preview)
// 2. which experiment template they are part of
func Images(r *rollout.RolloutInfo) []ImageInfo {
	var images []ImageInfo
	for _, rsInfo := range r.ReplicaSets {
		if rsInfo.Replicas > 0 {
			for _, image := range rsInfo.Images {
				newImage := ImageInfo{
					Image: image,
				}
				if rsInfo.Canary {
					newImage.Tags = append(newImage.Tags, InfoTagCanary)
				}
				if rsInfo.Stable {
					newImage.Tags = append(newImage.Tags, InfoTagStable)
				}
				if rsInfo.Active {
					newImage.Tags = append(newImage.Tags, InfoTagActive)
				}
				if rsInfo.Preview {
```

---

</SwmSnippet>

### Revisions

The <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="220:2:2" line-data="func Revisions(r *rollout.RolloutInfo) []int {">`Revisions`</SwmToken> function returns a list of revisions associated with the rollout, sorted in reverse order. This helps in tracking the history and changes made to the rollout.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/info/rollout_info.go" line="220">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/info/rollout_info.go" pos="220:2:2" line-data="func Revisions(r *rollout.RolloutInfo) []int {">`Revisions`</SwmToken> function returns a list of revisions associated with the rollout, sorted in reverse order.

```go
func Revisions(r *rollout.RolloutInfo) []int {
	revisionMap := make(map[int]bool)
	for _, rsInfo := range r.ReplicaSets {
		revisionMap[int(rsInfo.Revision)] = true
	}
	for _, expInfo := range r.Experiments {
		revisionMap[int(expInfo.Revision)] = true
	}
	for _, arInfo := range r.AnalysisRuns {
		revisionMap[int(arInfo.Revision)] = true
	}
	revisions := make([]int, 0, len(revisionMap))
	for k := range revisionMap {
		revisions = append(revisions, k)
	}
	sort.Sort(sort.Reverse(sort.IntSlice(revisions)))
	return revisions
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
