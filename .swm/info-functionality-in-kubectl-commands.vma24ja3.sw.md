---
title: Info Functionality in Kubectl Commands
---
# Understanding Info

Info in Kubectl Commands refers to the functionality that provides detailed information about various Kubernetes resources managed by Argo Rollouts. It includes functions and types to gather and format metadata, status, and other relevant details for resources like Rollouts, <SwmToken path="pkg/kubectl-argo-rollouts/info/experiment_info.go" pos="35:3:3" line-data="	expInfo.ReplicaSets = GetReplicaSetInfo(exp.UID, nil, allReplicaSets, allPods)">`ReplicaSets`</SwmToken>, Pods, Experiments, and <SwmToken path="pkg/kubectl-argo-rollouts/info/experiment_info.go" pos="36:3:3" line-data="	expInfo.AnalysisRuns = getAnalysisRunInfo(exp.UID, allAnalysisRuns)">`AnalysisRuns`</SwmToken>.

## Constants and Tags

The <SwmToken path="pkg/kubectl-argo-rollouts/info/info.go" pos="1:2:2" line-data="package info">`info`</SwmToken> package defines constants for various icons and tags used to represent the state and type of resources, such as <SwmToken path="pkg/kubectl-argo-rollouts/info/experiment_info.go" pos="87:3:3" line-data="		return IconOK">`IconOK`</SwmToken>, <SwmToken path="pkg/kubectl-argo-rollouts/info/experiment_info.go" pos="93:3:3" line-data="		return IconWarning">`IconWarning`</SwmToken>, <SwmToken path="pkg/kubectl-argo-rollouts/info/info.go" pos="28:1:1" line-data="	InfoTagCanary  = &quot;canary&quot;">`InfoTagCanary`</SwmToken>, and <SwmToken path="pkg/kubectl-argo-rollouts/info/info.go" pos="29:1:1" line-data="	InfoTagStable  = &quot;stable&quot;">`InfoTagStable`</SwmToken>.

## Functions Overview

Functions like <SwmToken path="pkg/kubectl-argo-rollouts/info/info.go" pos="43:2:2" line-data="func Age(m v1.ObjectMeta) string {">`Age`</SwmToken>, <SwmToken path="pkg/kubectl-argo-rollouts/info/info.go" pos="47:2:2" line-data="func ownerRef(ownerRefs []metav1.OwnerReference, uids []types.UID) *metav1.OwnerReference {">`ownerRef`</SwmToken>, and <SwmToken path="pkg/kubectl-argo-rollouts/info/info.go" pos="58:2:2" line-data="func parseRevision(annotations_ map[string]string) int {">`parseRevision`</SwmToken> are used to compute and retrieve specific pieces of information about the resources.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/info/info.go" line="47">

---

## Associating Pods with <SwmToken path="pkg/kubectl-argo-rollouts/info/experiment_info.go" pos="35:3:3" line-data="	expInfo.ReplicaSets = GetReplicaSetInfo(exp.UID, nil, allReplicaSets, allPods)">`ReplicaSets`</SwmToken>

The <SwmToken path="pkg/kubectl-argo-rollouts/info/info.go" pos="47:2:2" line-data="func ownerRef(ownerRefs []metav1.OwnerReference, uids []types.UID) *metav1.OwnerReference {">`ownerRef`</SwmToken> function is used to match owner references for associating resources like Pods with their respective <SwmToken path="pkg/kubectl-argo-rollouts/info/experiment_info.go" pos="35:3:3" line-data="	expInfo.ReplicaSets = GetReplicaSetInfo(exp.UID, nil, allReplicaSets, allPods)">`ReplicaSets`</SwmToken>.

```go
func ownerRef(ownerRefs []metav1.OwnerReference, uids []types.UID) *metav1.OwnerReference {
	for _, ownerRef := range ownerRefs {
		for _, uid := range uids {
			if ownerRef.UID == uid {
				return &ownerRef
			}
		}
	}
	return nil
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/kubectl-argo-rollouts/info/experiment_info.go" line="16">

---

## Creating Experiment Info

The <SwmToken path="pkg/kubectl-argo-rollouts/info/experiment_info.go" pos="16:2:2" line-data="func NewExperimentInfo(">`NewExperimentInfo`</SwmToken> function creates a new <SwmToken path="pkg/kubectl-argo-rollouts/info/experiment_info.go" pos="21:5:5" line-data=") *rollout.ExperimentInfo {">`ExperimentInfo`</SwmToken> object. It gathers metadata, status, and other relevant details about an experiment, including associated <SwmToken path="pkg/kubectl-argo-rollouts/info/experiment_info.go" pos="35:3:3" line-data="	expInfo.ReplicaSets = GetReplicaSetInfo(exp.UID, nil, allReplicaSets, allPods)">`ReplicaSets`</SwmToken> and <SwmToken path="pkg/kubectl-argo-rollouts/info/experiment_info.go" pos="36:3:3" line-data="	expInfo.AnalysisRuns = getAnalysisRunInfo(exp.UID, allAnalysisRuns)">`AnalysisRuns`</SwmToken>.

```go
func NewExperimentInfo(
	exp *v1alpha1.Experiment,
	allReplicaSets []*appsv1.ReplicaSet,
	allAnalysisRuns []*v1alpha1.AnalysisRun,
	allPods []*corev1.Pod,
) *rollout.ExperimentInfo {

	expInfo := rollout.ExperimentInfo{
		ObjectMeta: &v1.ObjectMeta{
			Name:              exp.Name,
			Namespace:         exp.Namespace,
			CreationTimestamp: exp.CreationTimestamp,
			UID:               exp.UID,
		},
		Status:  string(exp.Status.Phase),
		Message: exp.Status.Message,
	}
	expInfo.Icon = analysisIcon(exp.Status.Phase)
	expInfo.Revision = int64(parseRevision(exp.ObjectMeta.Annotations))
	expInfo.ReplicaSets = GetReplicaSetInfo(exp.UID, nil, allReplicaSets, allPods)
	expInfo.AnalysisRuns = getAnalysisRunInfo(exp.UID, allAnalysisRuns)
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/kubectl-argo-rollouts/info/experiment_info.go" line="40">

---

## Retrieving Experiment Info

The <SwmToken path="pkg/kubectl-argo-rollouts/info/experiment_info.go" pos="40:2:2" line-data="func getExperimentInfo(">`getExperimentInfo`</SwmToken> function retrieves detailed information about experiments related to a specific Rollout. It filters experiments by owner references and sorts them by revision and creation timestamp.

```go
func getExperimentInfo(
	ro *v1alpha1.Rollout,
	allExperiments []*v1alpha1.Experiment,
	allReplicaSets []*appsv1.ReplicaSet,
	allAnalysisRuns []*v1alpha1.AnalysisRun,
	allPods []*corev1.Pod,
) []*rollout.ExperimentInfo {

	var expInfos []*rollout.ExperimentInfo
	for _, exp := range allExperiments {
		if ownerRef(exp.OwnerReferences, []types.UID{ro.UID}) == nil {
			continue
		}
		expInfo := NewExperimentInfo(exp, allReplicaSets, allAnalysisRuns, allPods)
		expInfos = append(expInfos, expInfo)
	}
	sort.Slice(expInfos[:], func(i, j int) bool {
		if expInfos[i].Revision > expInfos[j].Revision {
			return true
		}
		return expInfos[i].ObjectMeta.CreationTimestamp.Before(&expInfos[j].ObjectMeta.CreationTimestamp)
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/kubectl-argo-rollouts/info/info.go" line="58">

---

## Parsing Revision

The <SwmToken path="pkg/kubectl-argo-rollouts/info/info.go" pos="58:2:2" line-data="func parseRevision(annotations_ map[string]string) int {">`parseRevision`</SwmToken> function retrieves the revision number from the annotations of a resource.

```go
func parseRevision(annotations_ map[string]string) int {
	if annotations_ != nil {
		if revision, err := strconv.Atoi(annotations_[annotations.RevisionAnnotation]); err == nil {
			return revision
		}
	}
	return 0
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/kubectl-argo-rollouts/info/experiment_info.go" line="84">

---

## Analysis Icon

The <SwmToken path="pkg/kubectl-argo-rollouts/info/experiment_info.go" pos="84:2:2" line-data="func analysisIcon(status v1alpha1.AnalysisPhase) string {">`analysisIcon`</SwmToken> function returns the appropriate icon based on the status of an analysis phase.

```go
func analysisIcon(status v1alpha1.AnalysisPhase) string {
	switch status {
	case v1alpha1.AnalysisPhaseSuccessful:
		return IconOK
	case v1alpha1.AnalysisPhaseInconclusive:
		return IconUnknown
	case v1alpha1.AnalysisPhaseFailed:
		return IconBad
	case v1alpha1.AnalysisPhaseError:
		return IconWarning
	case v1alpha1.AnalysisPhaseRunning:
		return IconProgressing
	case v1alpha1.AnalysisPhasePending:
		return IconWaiting
	}
	return " "
}
```

---

</SwmSnippet>

## Adding Pod Infos

The <SwmToken path="pkg/kubectl-argo-rollouts/info/pod_info.go" pos="15:2:2" line-data="func addPodInfos(rsInfos []*rollout.ReplicaSetInfo, allPods []*corev1.Pod) []*rollout.ReplicaSetInfo {">`addPodInfos`</SwmToken> function associates pods with their respective <SwmToken path="pkg/kubectl-argo-rollouts/info/experiment_info.go" pos="35:3:3" line-data="	expInfo.ReplicaSets = GetReplicaSetInfo(exp.UID, nil, allReplicaSets, allPods)">`ReplicaSets`</SwmToken> by matching owner references and updates the <SwmToken path="pkg/kubectl-argo-rollouts/info/experiment_info.go" pos="18:8:8" line-data="	allReplicaSets []*appsv1.ReplicaSet,">`ReplicaSet`</SwmToken> information accordingly.

## Testing Info Functions

The <SwmPath>[pkg/kubectl-argo-rollouts/info/info_test.go](pkg/kubectl-argo-rollouts/info/info_test.go)</SwmPath> file contains tests to ensure the correctness of the information retrieval and formatting functions, validating scenarios like canary rollouts, blue-green deployments, and experiment analysis.

## Rollouts Get Command

This command consists of multiple subcommands which can be used to get extended information about a rollout or experiment.

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
