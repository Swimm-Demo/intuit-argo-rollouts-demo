---
title: ClusterAnalysisTemplate Overview
---
# Overview

<SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" pos="107:23:23" line-data="func (c *clusterAnalysisTemplates) Create(ctx context.Context, clusterAnalysisTemplate *v1alpha1.ClusterAnalysisTemplate, opts v1.CreateOptions) (result *v1alpha1.ClusterAnalysisTemplate, err error) {">`ClusterAnalysisTemplate`</SwmToken> is a cluster-scoped resource that defines how to perform a canary analysis. It includes the metrics to be evaluated, their frequency, and the criteria for success or failure. This resource is used to share analysis templates across multiple rollouts in different namespaces, avoiding the need to duplicate the same template in every namespace.

# Clientset Interface

In the Clientset, the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" pos="33:16:16" line-data="// ClusterAnalysisTemplatesGetter has a method to return a ClusterAnalysisTemplateInterface.">`ClusterAnalysisTemplateInterface`</SwmToken> provides methods to create, update, delete, get, list, watch, and patch <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" pos="107:23:23" line-data="func (c *clusterAnalysisTemplates) Create(ctx context.Context, clusterAnalysisTemplate *v1alpha1.ClusterAnalysisTemplate, opts v1.CreateOptions) (result *v1alpha1.ClusterAnalysisTemplate, err error) {">`ClusterAnalysisTemplate`</SwmToken> resources. The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" pos="107:6:6" line-data="func (c *clusterAnalysisTemplates) Create(ctx context.Context, clusterAnalysisTemplate *v1alpha1.ClusterAnalysisTemplate, opts v1.CreateOptions) (result *v1alpha1.ClusterAnalysisTemplate, err error) {">`clusterAnalysisTemplates`</SwmToken> struct implements the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" pos="33:16:16" line-data="// ClusterAnalysisTemplatesGetter has a method to return a ClusterAnalysisTemplateInterface.">`ClusterAnalysisTemplateInterface`</SwmToken> and interacts with the Kubernetes API server using a REST client.

# Initialization

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" pos="57:2:2" line-data="// newClusterAnalysisTemplates returns a ClusterAnalysisTemplates">`newClusterAnalysisTemplates`</SwmToken> function initializes a new instance of <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" pos="107:6:6" line-data="func (c *clusterAnalysisTemplates) Create(ctx context.Context, clusterAnalysisTemplate *v1alpha1.ClusterAnalysisTemplate, opts v1.CreateOptions) (result *v1alpha1.ClusterAnalysisTemplate, err error) {">`clusterAnalysisTemplates`</SwmToken> with a given REST client.

# Creating a <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" pos="107:23:23" line-data="func (c *clusterAnalysisTemplates) Create(ctx context.Context, clusterAnalysisTemplate *v1alpha1.ClusterAnalysisTemplate, opts v1.CreateOptions) (result *v1alpha1.ClusterAnalysisTemplate, err error) {">`ClusterAnalysisTemplate`</SwmToken>

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" pos="106:2:2" line-data="// Create takes the representation of a clusterAnalysisTemplate and creates it.  Returns the server&#39;s representation of the clusterAnalysisTemplate, and an error, if there is any.">`Create`</SwmToken> method sends a POST request to the Kubernetes API server to create a new <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" pos="107:23:23" line-data="func (c *clusterAnalysisTemplates) Create(ctx context.Context, clusterAnalysisTemplate *v1alpha1.ClusterAnalysisTemplate, opts v1.CreateOptions) (result *v1alpha1.ClusterAnalysisTemplate, err error) {">`ClusterAnalysisTemplate`</SwmToken> resource.

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" line="106">

---

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" pos="106:2:2" line-data="// Create takes the representation of a clusterAnalysisTemplate and creates it.  Returns the server&#39;s representation of the clusterAnalysisTemplate, and an error, if there is any.">`Create`</SwmToken> method in the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" pos="107:6:6" line-data="func (c *clusterAnalysisTemplates) Create(ctx context.Context, clusterAnalysisTemplate *v1alpha1.ClusterAnalysisTemplate, opts v1.CreateOptions) (result *v1alpha1.ClusterAnalysisTemplate, err error) {">`clusterAnalysisTemplates`</SwmToken> struct takes the representation of a <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" pos="107:23:23" line-data="func (c *clusterAnalysisTemplates) Create(ctx context.Context, clusterAnalysisTemplate *v1alpha1.ClusterAnalysisTemplate, opts v1.CreateOptions) (result *v1alpha1.ClusterAnalysisTemplate, err error) {">`ClusterAnalysisTemplate`</SwmToken> and creates it. It returns the server's representation of the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" pos="107:23:23" line-data="func (c *clusterAnalysisTemplates) Create(ctx context.Context, clusterAnalysisTemplate *v1alpha1.ClusterAnalysisTemplate, opts v1.CreateOptions) (result *v1alpha1.ClusterAnalysisTemplate, err error) {">`ClusterAnalysisTemplate`</SwmToken> and an error if there is any.

```go
// Create takes the representation of a clusterAnalysisTemplate and creates it.  Returns the server's representation of the clusterAnalysisTemplate, and an error, if there is any.
func (c *clusterAnalysisTemplates) Create(ctx context.Context, clusterAnalysisTemplate *v1alpha1.ClusterAnalysisTemplate, opts v1.CreateOptions) (result *v1alpha1.ClusterAnalysisTemplate, err error) {
	result = &v1alpha1.ClusterAnalysisTemplate{}
	err = c.client.Post().
		Resource("clusteranalysistemplates").
		VersionedParams(&opts, scheme.ParameterCodec).
		Body(clusterAnalysisTemplate).
		Do(ctx).
		Into(result)
	return
}
```

---

</SwmSnippet>

# Usage in Rollouts

A Rollout can reference a cluster-scoped <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="39:2:2" line-data="type AnalysisTemplate struct {">`AnalysisTemplate`</SwmToken> called a <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/clusteranalysistemplate.go" pos="107:23:23" line-data="func (c *clusterAnalysisTemplates) Create(ctx context.Context, clusterAnalysisTemplate *v1alpha1.ClusterAnalysisTemplate, opts v1.CreateOptions) (result *v1alpha1.ClusterAnalysisTemplate, err error) {">`ClusterAnalysisTemplate`</SwmToken>. This is useful when you want to share an <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="39:2:2" line-data="type AnalysisTemplate struct {">`AnalysisTemplate`</SwmToken> across multiple Rollouts in different namespaces and avoid duplicating the same template in every namespace.

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
