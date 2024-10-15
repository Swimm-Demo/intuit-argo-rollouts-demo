---
title: Getting Started with Experiment in Clientset
---
# Introduction

The Experiment in Clientset is a resource that allows users to run ephemeral instances of one or more <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="922:1:1" line-data="	ReplicaSets          []*ReplicaSetInfo  `protobuf:&quot;bytes,6,rep,name=replicaSets,proto3&quot; json:&quot;replicaSets,omitempty&quot;`">`ReplicaSets`</SwmToken>. These <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="922:1:1" line-data="	ReplicaSets          []*ReplicaSetInfo  `protobuf:&quot;bytes,6,rep,name=replicaSets,proto3&quot; json:&quot;replicaSets,omitempty&quot;`">`ReplicaSets`</SwmToken> can be used to test new versions of applications or configurations before they are rolled out to production. The Experiment resource can also launch <SwmToken path="pkg/client/listers/rollouts/v1alpha1/analysisrun.go" pos="35:1:1" line-data="	AnalysisRuns(namespace string) AnalysisRunNamespaceLister">`AnalysisRuns`</SwmToken> alongside the <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="922:1:1" line-data="	ReplicaSets          []*ReplicaSetInfo  `protobuf:&quot;bytes,6,rep,name=replicaSets,proto3&quot; json:&quot;replicaSets,omitempty&quot;`">`ReplicaSets`</SwmToken> to verify that the new <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="922:1:1" line-data="	ReplicaSets          []*ReplicaSetInfo  `protobuf:&quot;bytes,6,rep,name=replicaSets,proto3&quot; json:&quot;replicaSets,omitempty&quot;`">`ReplicaSets`</SwmToken> are functioning as expected.

# Traffic Management

A Service routing traffic to the Experiment ReplicaSet is generated if a weight is specified or if the Service attribute for the experiment is set. This allows for traffic management during the experiment.

# <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/experiment.go" pos="33:16:16" line-data="// ExperimentsGetter has a method to return a ExperimentInterface.">`ExperimentInterface`</SwmToken>

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/experiment.go" pos="33:16:16" line-data="// ExperimentsGetter has a method to return a ExperimentInterface.">`ExperimentInterface`</SwmToken> in the Clientset provides methods to create, update, delete, and retrieve Experiment resources. It also supports listing and watching Experiment resources. The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/experiment.go" pos="68:6:6" line-data="func (c *experiments) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.Experiment, err error) {">`experiments`</SwmToken> struct implements the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/experiment.go" pos="33:16:16" line-data="// ExperimentsGetter has a method to return a ExperimentInterface.">`ExperimentInterface`</SwmToken> and interacts with the Kubernetes API server to manage Experiment resources using a REST client.

# Creating an Experiment

To create an Experiment resource, use the `kubectl `<SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/experiment.go" pos="25:10:10" line-data="	v1alpha1 &quot;github.com/argoproj/argo-rollouts/pkg/apis/rollouts/v1alpha1&quot;">`argo`</SwmToken>` `<SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/rollout.go" pos="54:2:2" line-data="type rollouts struct {">`rollouts`</SwmToken>` `<SwmToken path="utils/ingress/wrapper.go" pos="507:9:9" line-data="func (w *IngressWrap) create(ctx context.Context, namespace string, ingress *v1.Ingress, opts metav1.CreateOptions) (*Ingress, error) {">`create`</SwmToken> command.

# Getting Experiment Details

To retrieve details about an Experiment, use the `kubectl `<SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/experiment.go" pos="25:10:10" line-data="	v1alpha1 &quot;github.com/argoproj/argo-rollouts/pkg/apis/rollouts/v1alpha1&quot;">`argo`</SwmToken>` `<SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/rollout.go" pos="54:2:2" line-data="type rollouts struct {">`rollouts`</SwmToken>` `<SwmToken path="utils/ingress/wrapper.go" pos="454:9:9" line-data="func (w *IngressWrap) get(ctx context.Context, namespace, name string, opts metav1.GetOptions) (*Ingress, error) {">`get`</SwmToken>` `<SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/experiment.go" pos="67:12:12" line-data="// Get takes name of the experiment, and returns the corresponding experiment object, and an error if there is any.">`experiment`</SwmToken> command.

# Experiment Spec

The Experiment Spec section provides an example of an experiment that creates two <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="922:1:1" line-data="	ReplicaSets          []*ReplicaSetInfo  `protobuf:&quot;bytes,6,rep,name=replicaSets,proto3&quot; json:&quot;replicaSets,omitempty&quot;`">`ReplicaSets`</SwmToken> with 1 replica each and runs them for 20 minutes once they both become available. Additionally, several <SwmToken path="pkg/client/listers/rollouts/v1alpha1/analysisrun.go" pos="35:1:1" line-data="	AnalysisRuns(namespace string) AnalysisRunNamespaceLister">`AnalysisRuns`</SwmToken> are run to perform analysis against the pods of the Experiment.

# Main Functions

There are several main functions in this folder. Some of them are Create, Update, Get, and List. We will dive a little into Create and Update.

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/experiment.go" line="112">

---

## Create

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/experiment.go" pos="112:2:2" line-data="// Create takes the representation of a experiment and creates it.  Returns the server&#39;s representation of the experiment, and an error, if there is any.">`Create`</SwmToken> function takes the representation of an experiment and creates it. It returns the server's representation of the experiment and an error if there is any.

```go
// Create takes the representation of a experiment and creates it.  Returns the server's representation of the experiment, and an error, if there is any.
func (c *experiments) Create(ctx context.Context, experiment *v1alpha1.Experiment, opts v1.CreateOptions) (result *v1alpha1.Experiment, err error) {
	result = &v1alpha1.Experiment{}
	err = c.client.Post().
		Namespace(c.ns).
		Resource("experiments").
		VersionedParams(&opts, scheme.ParameterCodec).
		Body(experiment).
		Do(ctx).
		Into(result)
	return
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/experiment.go" line="125">

---

## Update

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/experiment.go" pos="125:2:2" line-data="// Update takes the representation of a experiment and updates it. Returns the server&#39;s representation of the experiment, and an error, if there is any.">`Update`</SwmToken> function takes the representation of an experiment and updates it. It returns the server's representation of the experiment and an error if there is any.

```go
// Update takes the representation of a experiment and updates it. Returns the server's representation of the experiment, and an error, if there is any.
func (c *experiments) Update(ctx context.Context, experiment *v1alpha1.Experiment, opts v1.UpdateOptions) (result *v1alpha1.Experiment, err error) {
	result = &v1alpha1.Experiment{}
	err = c.client.Put().
		Namespace(c.ns).
		Resource("experiments").
		Name(experiment.Name).
		VersionedParams(&opts, scheme.ParameterCodec).
		Body(experiment).
		Do(ctx).
		Into(result)
	return
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/experiment.go" line="67">

---

## Get

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/experiment.go" pos="67:2:2" line-data="// Get takes name of the experiment, and returns the corresponding experiment object, and an error if there is any.">`Get`</SwmToken> function takes the name of the experiment and returns the corresponding experiment object and an error if there is any.

```go
// Get takes name of the experiment, and returns the corresponding experiment object, and an error if there is any.
func (c *experiments) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.Experiment, err error) {
	result = &v1alpha1.Experiment{}
	err = c.client.Get().
		Namespace(c.ns).
		Resource("experiments").
		Name(name).
		VersionedParams(&options, scheme.ParameterCodec).
		Do(ctx).
		Into(result)
	return
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/experiment.go" line="80">

---

## List

The `List` function takes label and field selectors and returns the list of experiments that match those selectors.

```go
// List takes label and field selectors, and returns the list of Experiments that match those selectors.
func (c *experiments) List(ctx context.Context, opts v1.ListOptions) (result *v1alpha1.ExperimentList, err error) {
	var timeout time.Duration
	if opts.TimeoutSeconds != nil {
		timeout = time.Duration(*opts.TimeoutSeconds) * time.Second
	}
	result = &v1alpha1.ExperimentList{}
	err = c.client.Get().
		Namespace(c.ns).
		Resource("experiments").
		VersionedParams(&opts, scheme.ParameterCodec).
		Timeout(timeout).
		Do(ctx).
		Into(result)
	return
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
