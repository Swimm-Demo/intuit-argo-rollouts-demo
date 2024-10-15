---
title: Fake Clients for Testing
---
# Overview

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_experiment.go" pos="34:1:1" line-data="	Fake *FakeArgoprojV1alpha1">`Fake`</SwmToken> package is used to create mock implementations of the client interfaces for testing purposes. It provides fake clients for various resources like <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/rollouts_client.go" pos="55:9:9" line-data="func (c *ArgoprojV1alpha1Client) Experiments(namespace string) ExperimentInterface {">`Experiments`</SwmToken>, <SwmToken path="pkg/client/listers/rollouts/v1alpha1/analysisrun.go" pos="35:1:1" line-data="	AnalysisRuns(namespace string) AnalysisRunNamespaceLister">`AnalysisRuns`</SwmToken>, <SwmToken path="pkg/client/listers/rollouts/v1alpha1/analysistemplate.go" pos="35:1:1" line-data="	AnalysisTemplates(namespace string) AnalysisTemplateNamespaceLister">`AnalysisTemplates`</SwmToken>, <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/rollouts_client.go" pos="59:9:9" line-data="func (c *ArgoprojV1alpha1Client) Rollouts(namespace string) RolloutInterface {">`Rollouts`</SwmToken>, and <SwmToken path="pkg/apis/rollouts/validation/validation_references.go" pos="38:1:1" line-data="	ClusterAnalysisTemplates []*v1alpha1.ClusterAnalysisTemplate">`ClusterAnalysisTemplates`</SwmToken>. These fake clients simulate the behavior of the actual clients, allowing developers to test their code without needing a real Kubernetes cluster.

# How Fake Clients Work

The fake clients use the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_rollouts_client.go" pos="28:2:2" line-data="	*testing.Fake">`testing`</SwmToken> package from <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_experiment.go" pos="29:4:10" line-data="	testing &quot;k8s.io/client-go/testing&quot;">`k8s.io/client-go`</SwmToken> to invoke actions and return predefined responses. This allows developers to simulate API calls and test their code in a controlled environment.

# <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_experiment.go" pos="32:2:2" line-data="// FakeExperiments implements ExperimentInterface">`FakeExperiments`</SwmToken> Struct

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_experiment.go" pos="32:2:2" line-data="// FakeExperiments implements ExperimentInterface">`FakeExperiments`</SwmToken> struct implements the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_experiment.go" pos="32:6:6" line-data="// FakeExperiments implements ExperimentInterface">`ExperimentInterface`</SwmToken> and provides methods like <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="46:1:1" line-data="	Get(ctx context.Context, name string, opts v1.GetOptions) (*v1alpha1.AnalysisRun, error)">`Get`</SwmToken>, `List`, <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="41:1:1" line-data="	Create(ctx context.Context, analysisRun *v1alpha1.AnalysisRun, opts v1.CreateOptions) (*v1alpha1.AnalysisRun, error)">`Create`</SwmToken>, <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="42:1:1" line-data="	Update(ctx context.Context, analysisRun *v1alpha1.AnalysisRun, opts v1.UpdateOptions) (*v1alpha1.AnalysisRun, error)">`Update`</SwmToken>, <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="44:1:1" line-data="	Delete(ctx context.Context, name string, opts v1.DeleteOptions) error">`Delete`</SwmToken>, and <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="49:1:1" line-data="	Patch(ctx context.Context, name string, pt types.PatchType, data []byte, opts v1.PatchOptions, subresources ...string) (result *v1alpha1.AnalysisRun, err error)">`Patch`</SwmToken>. These methods use the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_experiment.go" pos="45:1:1" line-data="		Invokes(testing.NewGetAction(experimentsResource, c.ns, name), &amp;v1alpha1.Experiment{})">`Invokes`</SwmToken> function from the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_rollouts_client.go" pos="28:2:2" line-data="	*testing.Fake">`testing`</SwmToken> package to simulate API calls and return fake responses.

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_experiment.go" line="32">

---

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_experiment.go" pos="32:2:2" line-data="// FakeExperiments implements ExperimentInterface">`FakeExperiments`</SwmToken> struct is defined here and is used to simulate API calls for experiments.

```go
// FakeExperiments implements ExperimentInterface
type FakeExperiments struct {
	Fake *FakeArgoprojV1alpha1
	ns   string
}
```

---

</SwmSnippet>

# <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_experiment.go" pos="34:4:4" line-data="	Fake *FakeArgoprojV1alpha1">`FakeArgoprojV1alpha1`</SwmToken> Struct

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_experiment.go" pos="34:4:4" line-data="	Fake *FakeArgoprojV1alpha1">`FakeArgoprojV1alpha1`</SwmToken> struct is used to create fake clients for various resources like <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/rollouts_client.go" pos="55:9:9" line-data="func (c *ArgoprojV1alpha1Client) Experiments(namespace string) ExperimentInterface {">`Experiments`</SwmToken>, <SwmToken path="pkg/client/listers/rollouts/v1alpha1/analysisrun.go" pos="35:1:1" line-data="	AnalysisRuns(namespace string) AnalysisRunNamespaceLister">`AnalysisRuns`</SwmToken>, and <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/rollouts_client.go" pos="59:9:9" line-data="func (c *ArgoprojV1alpha1Client) Rollouts(namespace string) RolloutInterface {">`Rollouts`</SwmToken>. It leverages the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_rollouts_client.go" pos="28:2:4" line-data="	*testing.Fake">`testing.Fake`</SwmToken> struct to simulate the behavior of the actual clients.

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_rollouts_client.go" line="27">

---

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_rollouts_client.go" pos="27:2:2" line-data="type FakeArgoprojV1alpha1 struct {">`FakeArgoprojV1alpha1`</SwmToken> struct is defined here and is used to create fake clients for various resources.

```go
type FakeArgoprojV1alpha1 struct {
	*testing.Fake
}
```

---

</SwmSnippet>

# <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_rollout.go" pos="32:2:2" line-data="// FakeRollouts implements RolloutInterface">`FakeRollouts`</SwmToken> Struct

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_rollout.go" pos="32:2:2" line-data="// FakeRollouts implements RolloutInterface">`FakeRollouts`</SwmToken> struct implements the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_rollout.go" pos="32:6:6" line-data="// FakeRollouts implements RolloutInterface">`RolloutInterface`</SwmToken> and provides methods to simulate API calls for rollouts. This allows developers to test rollout-related functionality without needing a real Kubernetes cluster.

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_rollout.go" line="32">

---

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/fake/fake_rollout.go" pos="32:2:2" line-data="// FakeRollouts implements RolloutInterface">`FakeRollouts`</SwmToken> struct is defined here and is used to simulate API calls for rollouts.

```go
// FakeRollouts implements RolloutInterface
type FakeRollouts struct {
	Fake *FakeArgoprojV1alpha1
	ns   string
}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
