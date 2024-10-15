---
title: Listers in Client Library
---
# What are Listers in Client Library

Listers are used to list and retrieve Kubernetes resources in a <SwmToken path="pkg/client/listers/rollouts/v1alpha1/experiment.go" pos="29:18:20" line-data="// All objects returned here must be treated as read-only.">`read-only`</SwmToken> manner. They provide methods to list all resources of a specific type or to get resources within a specific namespace.

## <SwmToken path="pkg/client/listers/rollouts/v1alpha1/experiment.go" pos="28:2:2" line-data="// ExperimentLister helps list Experiments.">`ExperimentLister`</SwmToken> Interface

The <SwmToken path="pkg/client/listers/rollouts/v1alpha1/experiment.go" pos="28:2:2" line-data="// ExperimentLister helps list Experiments.">`ExperimentLister`</SwmToken> interface defines methods to list all <SwmToken path="pkg/client/listers/rollouts/v1alpha1/experiment.go" pos="28:8:8" line-data="// ExperimentLister helps list Experiments.">`Experiments`</SwmToken> or to get <SwmToken path="pkg/client/listers/rollouts/v1alpha1/experiment.go" pos="28:8:8" line-data="// ExperimentLister helps list Experiments.">`Experiments`</SwmToken> within a namespace. This interface ensures that all objects returned are treated as <SwmToken path="pkg/client/listers/rollouts/v1alpha1/experiment.go" pos="29:18:20" line-data="// All objects returned here must be treated as read-only.">`read-only`</SwmToken>.

<SwmSnippet path="/pkg/client/listers/rollouts/v1alpha1/experiment.go" line="28">

---

The <SwmToken path="pkg/client/listers/rollouts/v1alpha1/experiment.go" pos="28:2:2" line-data="// ExperimentLister helps list Experiments.">`ExperimentLister`</SwmToken> interface provides methods to list all <SwmToken path="pkg/client/listers/rollouts/v1alpha1/experiment.go" pos="28:8:8" line-data="// ExperimentLister helps list Experiments.">`Experiments`</SwmToken> and to get <SwmToken path="pkg/client/listers/rollouts/v1alpha1/experiment.go" pos="28:8:8" line-data="// ExperimentLister helps list Experiments.">`Experiments`</SwmToken> within a namespace. This ensures that the resources are accessed in a <SwmToken path="pkg/client/listers/rollouts/v1alpha1/experiment.go" pos="29:18:20" line-data="// All objects returned here must be treated as read-only.">`read-only`</SwmToken> manner.

```go
// ExperimentLister helps list Experiments.
// All objects returned here must be treated as read-only.
type ExperimentLister interface {
	// List lists all Experiments in the indexer.
	// Objects returned here must be treated as read-only.
	List(selector labels.Selector) (ret []*v1alpha1.Experiment, err error)
	// Experiments returns an object that can list and get Experiments.
	Experiments(namespace string) ExperimentNamespaceLister
	ExperimentListerExpansion
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/listers/rollouts/v1alpha1/experiment.go" line="39">

---

The <SwmToken path="pkg/client/listers/rollouts/v1alpha1/experiment.go" pos="39:2:2" line-data="// experimentLister implements the ExperimentLister interface.">`experimentLister`</SwmToken> struct implements the <SwmToken path="pkg/client/listers/rollouts/v1alpha1/experiment.go" pos="39:8:8" line-data="// experimentLister implements the ExperimentLister interface.">`ExperimentLister`</SwmToken> interface and uses an indexer to manage the cached resources.

```go
// experimentLister implements the ExperimentLister interface.
type experimentLister struct {
	indexer cache.Indexer
}
```

---

</SwmSnippet>

## Lister Endpoints

Lister endpoints provide specific methods to list and get resources. These methods are implemented in various lister interfaces and structs.

### List Method

The `List` function in the <SwmToken path="controller/metrics/metrics.go" pos="47:1:1" line-data="	ClusterAnalysisTemplateLister rolloutlister.ClusterAnalysisTemplateLister">`ClusterAnalysisTemplateLister`</SwmToken> interface lists all <SwmToken path="pkg/client/listers/rollouts/v1alpha1/clusteranalysistemplate.go" pos="50:8:8" line-data="// List lists all ClusterAnalysisTemplates in the indexer.">`ClusterAnalysisTemplates`</SwmToken> in the indexer. It uses the <SwmToken path="pkg/client/listers/rollouts/v1alpha1/clusteranalysistemplate.go" pos="52:5:7" line-data="	err = cache.ListAll(s.indexer, selector, func(m interface{}) {">`cache.ListAll`</SwmToken> method to retrieve the items based on the provided selector.

<SwmSnippet path="/pkg/client/listers/rollouts/v1alpha1/clusteranalysistemplate.go" line="50">

---

The `List` function lists all <SwmToken path="pkg/client/listers/rollouts/v1alpha1/clusteranalysistemplate.go" pos="50:8:8" line-data="// List lists all ClusterAnalysisTemplates in the indexer.">`ClusterAnalysisTemplates`</SwmToken> in the indexer using the <SwmToken path="pkg/client/listers/rollouts/v1alpha1/clusteranalysistemplate.go" pos="52:5:7" line-data="	err = cache.ListAll(s.indexer, selector, func(m interface{}) {">`cache.ListAll`</SwmToken> method.

```go
// List lists all ClusterAnalysisTemplates in the indexer.
func (s *clusterAnalysisTemplateLister) List(selector labels.Selector) (ret []*v1alpha1.ClusterAnalysisTemplate, err error) {
	err = cache.ListAll(s.indexer, selector, func(m interface{}) {
		ret = append(ret, m.(*v1alpha1.ClusterAnalysisTemplate))
	})
	return ret, err
```

---

</SwmSnippet>

### Get Method

The <SwmToken path="pkg/client/listers/rollouts/v1alpha1/clusteranalysistemplate.go" pos="58:2:2" line-data="// Get retrieves the ClusterAnalysisTemplate from the index for a given name.">`Get`</SwmToken> function in the <SwmToken path="controller/metrics/metrics.go" pos="47:1:1" line-data="	ClusterAnalysisTemplateLister rolloutlister.ClusterAnalysisTemplateLister">`ClusterAnalysisTemplateLister`</SwmToken> interface retrieves a <SwmToken path="pkg/client/listers/rollouts/v1alpha1/clusteranalysistemplate.go" pos="51:26:26" line-data="func (s *clusterAnalysisTemplateLister) List(selector labels.Selector) (ret []*v1alpha1.ClusterAnalysisTemplate, err error) {">`ClusterAnalysisTemplate`</SwmToken> by its name from the indexer. It uses the <SwmToken path="pkg/client/listers/rollouts/v1alpha1/experiment.go" pos="41:3:5" line-data="	indexer cache.Indexer">`cache.Indexer`</SwmToken>'s <SwmToken path="pkg/client/listers/rollouts/v1alpha1/clusteranalysistemplate.go" pos="60:15:15" line-data="	obj, exists, err := s.indexer.GetByKey(name)">`GetByKey`</SwmToken> method to fetch the item.

<SwmSnippet path="/pkg/client/listers/rollouts/v1alpha1/clusteranalysistemplate.go" line="58">

---

The <SwmToken path="pkg/client/listers/rollouts/v1alpha1/clusteranalysistemplate.go" pos="58:2:2" line-data="// Get retrieves the ClusterAnalysisTemplate from the index for a given name.">`Get`</SwmToken> function retrieves a <SwmToken path="pkg/client/listers/rollouts/v1alpha1/clusteranalysistemplate.go" pos="58:8:8" line-data="// Get retrieves the ClusterAnalysisTemplate from the index for a given name.">`ClusterAnalysisTemplate`</SwmToken> by its name from the indexer using the <SwmToken path="pkg/client/listers/rollouts/v1alpha1/experiment.go" pos="41:3:5" line-data="	indexer cache.Indexer">`cache.Indexer`</SwmToken>'s <SwmToken path="pkg/client/listers/rollouts/v1alpha1/clusteranalysistemplate.go" pos="60:15:15" line-data="	obj, exists, err := s.indexer.GetByKey(name)">`GetByKey`</SwmToken> method.

```go
// Get retrieves the ClusterAnalysisTemplate from the index for a given name.
func (s *clusterAnalysisTemplateLister) Get(name string) (*v1alpha1.ClusterAnalysisTemplate, error) {
	obj, exists, err := s.indexer.GetByKey(name)
	if err != nil {
		return nil, err
	}
	if !exists {
		return nil, errors.NewNotFound(v1alpha1.Resource("clusteranalysistemplate"), name)
	}
	return obj.(*v1alpha1.ClusterAnalysisTemplate), nil
}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
