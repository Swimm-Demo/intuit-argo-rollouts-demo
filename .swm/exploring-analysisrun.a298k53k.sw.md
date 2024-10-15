---
title: Exploring AnalysisRun
---
# Overview

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> resource allows you to run analysis tasks based on predefined metrics and thresholds. It is created from an <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="39:2:2" line-data="type AnalysisTemplate struct {">`AnalysisTemplate`</SwmToken> or a <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="19:2:2" line-data="type ClusterAnalysisTemplate struct {">`ClusterAnalysisTemplate`</SwmToken>, which define the metrics and expected results for the analysis.

# Creating an <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken>

To create an <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken>, use the command `kubectl `<SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="25:10:10" line-data="	v1alpha1 &quot;github.com/argoproj/argo-rollouts/pkg/apis/rollouts/v1alpha1&quot;">`argo`</SwmToken>` `<SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/rollout.go" pos="54:2:2" line-data="type rollouts struct {">`rollouts`</SwmToken>` `<SwmToken path="utils/ingress/wrapper.go" pos="507:9:9" line-data="func (w *IngressWrap) create(ctx context.Context, namespace string, ingress *v1.Ingress, opts metav1.CreateOptions) (*Ingress, error) {">`create`</SwmToken>` analysisrun [flags]`. This command can create a new <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> from an existing <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="39:2:2" line-data="type AnalysisTemplate struct {">`AnalysisTemplate`</SwmToken> resource or from an <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="39:2:2" line-data="type AnalysisTemplate struct {">`AnalysisTemplate`</SwmToken> file.

# Managing <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> Resources

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="33:16:16" line-data="// AnalysisRunsGetter has a method to return a AnalysisRunInterface.">`AnalysisRunInterface`</SwmToken> provides methods to work with <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> resources, including creating, updating, deleting, getting, listing, watching, and patching <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> resources.

# Initializing <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> Instances

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="59:2:2" line-data="// newAnalysisRuns returns a AnalysisRuns">`newAnalysisRuns`</SwmToken> function initializes an <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="60:16:16" line-data="func newAnalysisRuns(c *ArgoprojV1alpha1Client, namespace string) *analysisRuns {">`analysisRuns`</SwmToken> instance with a REST client and a namespace, allowing interaction with the Kubernetes API server to manage <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> resources.

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" line="59">

---

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="59:2:2" line-data="// newAnalysisRuns returns a AnalysisRuns">`newAnalysisRuns`</SwmToken> function returns an <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="60:16:16" line-data="func newAnalysisRuns(c *ArgoprojV1alpha1Client, namespace string) *analysisRuns {">`analysisRuns`</SwmToken> instance initialized with a REST client and a namespace.

```go
// newAnalysisRuns returns a AnalysisRuns
func newAnalysisRuns(c *ArgoprojV1alpha1Client, namespace string) *analysisRuns {
	return &analysisRuns{
		client: c.RESTClient(),
		ns:     namespace,
	}
}
```

---

</SwmSnippet>

# Main Functions

There are several main functions in <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken>. Some of them are <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="112:2:2" line-data="// Create takes the representation of a analysisRun and creates it.  Returns the server&#39;s representation of the analysisRun, and an error, if there is any.">`Create`</SwmToken>, <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="125:2:2" line-data="// Update takes the representation of a analysisRun and updates it. Returns the server&#39;s representation of the analysisRun, and an error, if there is any.">`Update`</SwmToken>, <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="155:2:2" line-data="// Delete takes name of the analysisRun and deletes it. Returns an error if one occurs.">`Delete`</SwmToken>, <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="67:2:2" line-data="// Get takes name of the analysisRun, and returns the corresponding analysisRun object, and an error if there is any.">`Get`</SwmToken>, `List`, <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="97:2:2" line-data="// Watch returns a watch.Interface that watches the requested analysisRuns.">`Watch`</SwmToken>, and <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="182:2:2" line-data="// Patch applies the patch and returns the patched analysisRun.">`Patch`</SwmToken>. We will dive a little into <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="112:2:2" line-data="// Create takes the representation of a analysisRun and creates it.  Returns the server&#39;s representation of the analysisRun, and an error, if there is any.">`Create`</SwmToken>, <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="125:2:2" line-data="// Update takes the representation of a analysisRun and updates it. Returns the server&#39;s representation of the analysisRun, and an error, if there is any.">`Update`</SwmToken>, and <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="155:2:2" line-data="// Delete takes name of the analysisRun and deletes it. Returns an error if one occurs.">`Delete`</SwmToken>.

## Create

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="112:2:2" line-data="// Create takes the representation of a analysisRun and creates it.  Returns the server&#39;s representation of the analysisRun, and an error, if there is any.">`Create`</SwmToken> function takes the representation of an <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> and creates it. It returns the server's representation of the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> and an error if there is any.

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" line="112">

---

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="112:2:2" line-data="// Create takes the representation of a analysisRun and creates it.  Returns the server&#39;s representation of the analysisRun, and an error, if there is any.">`Create`</SwmToken> function sends a POST request to create a new <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="113:23:23" line-data="func (c *analysisRuns) Create(ctx context.Context, analysisRun *v1alpha1.AnalysisRun, opts v1.CreateOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> and returns the server's representation of the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="113:23:23" line-data="func (c *analysisRuns) Create(ctx context.Context, analysisRun *v1alpha1.AnalysisRun, opts v1.CreateOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken>.

```go
// Create takes the representation of a analysisRun and creates it.  Returns the server's representation of the analysisRun, and an error, if there is any.
func (c *analysisRuns) Create(ctx context.Context, analysisRun *v1alpha1.AnalysisRun, opts v1.CreateOptions) (result *v1alpha1.AnalysisRun, err error) {
	result = &v1alpha1.AnalysisRun{}
	err = c.client.Post().
		Namespace(c.ns).
		Resource("analysisruns").
		VersionedParams(&opts, scheme.ParameterCodec).
		Body(analysisRun).
		Do(ctx).
		Into(result)
	return
}
```

---

</SwmSnippet>

## Update

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="125:2:2" line-data="// Update takes the representation of a analysisRun and updates it. Returns the server&#39;s representation of the analysisRun, and an error, if there is any.">`Update`</SwmToken> function takes the representation of an <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> and updates it. It returns the server's representation of the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> and an error if there is any.

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" line="125">

---

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="125:2:2" line-data="// Update takes the representation of a analysisRun and updates it. Returns the server&#39;s representation of the analysisRun, and an error, if there is any.">`Update`</SwmToken> function sends a PUT request to update an existing <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="126:23:23" line-data="func (c *analysisRuns) Update(ctx context.Context, analysisRun *v1alpha1.AnalysisRun, opts v1.UpdateOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> and returns the server's representation of the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="126:23:23" line-data="func (c *analysisRuns) Update(ctx context.Context, analysisRun *v1alpha1.AnalysisRun, opts v1.UpdateOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken>.

```go
// Update takes the representation of a analysisRun and updates it. Returns the server's representation of the analysisRun, and an error, if there is any.
func (c *analysisRuns) Update(ctx context.Context, analysisRun *v1alpha1.AnalysisRun, opts v1.UpdateOptions) (result *v1alpha1.AnalysisRun, err error) {
	result = &v1alpha1.AnalysisRun{}
	err = c.client.Put().
		Namespace(c.ns).
		Resource("analysisruns").
		Name(analysisRun.Name).
		VersionedParams(&opts, scheme.ParameterCodec).
		Body(analysisRun).
		Do(ctx).
		Into(result)
	return
```

---

</SwmSnippet>

## Delete

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="155:2:2" line-data="// Delete takes name of the analysisRun and deletes it. Returns an error if one occurs.">`Delete`</SwmToken> function takes the name of the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> and deletes it. It returns an error if one occurs.

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" line="155">

---

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="155:2:2" line-data="// Delete takes name of the analysisRun and deletes it. Returns an error if one occurs.">`Delete`</SwmToken> function sends a DELETE request to remove an <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> by name and returns an error if one occurs.

```go
// Delete takes name of the analysisRun and deletes it. Returns an error if one occurs.
func (c *analysisRuns) Delete(ctx context.Context, name string, opts v1.DeleteOptions) error {
	return c.client.Delete().
		Namespace(c.ns).
		Resource("analysisruns").
		Name(name).
		Body(&opts).
		Do(ctx).
		Error()
}
```

---

</SwmSnippet>

## Get

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="67:2:2" line-data="// Get takes name of the analysisRun, and returns the corresponding analysisRun object, and an error if there is any.">`Get`</SwmToken> function takes the name of the <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> and returns the corresponding <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> object and an error if there is any.

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" line="67">

---

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="67:2:2" line-data="// Get takes name of the analysisRun, and returns the corresponding analysisRun object, and an error if there is any.">`Get`</SwmToken> function sends a GET request to retrieve an <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> by name and returns the corresponding <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> object.

```go
// Get takes name of the analysisRun, and returns the corresponding analysisRun object, and an error if there is any.
func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {
	result = &v1alpha1.AnalysisRun{}
	err = c.client.Get().
		Namespace(c.ns).
		Resource("analysisruns").
		Name(name).
		VersionedParams(&options, scheme.ParameterCodec).
		Do(ctx).
		Into(result)
	return
}
```

---

</SwmSnippet>

## List

The `List` function takes label and field selectors and returns the list of <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="59:8:8" line-data="// newAnalysisRuns returns a AnalysisRuns">`AnalysisRuns`</SwmToken> that match those selectors.

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" line="80">

---

The `List` function sends a GET request with label and field selectors to retrieve a list of <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="80:25:25" line-data="// List takes label and field selectors, and returns the list of AnalysisRuns that match those selectors.">`AnalysisRuns`</SwmToken> that match those selectors.

```go
// List takes label and field selectors, and returns the list of AnalysisRuns that match those selectors.
func (c *analysisRuns) List(ctx context.Context, opts v1.ListOptions) (result *v1alpha1.AnalysisRunList, err error) {
	var timeout time.Duration
	if opts.TimeoutSeconds != nil {
		timeout = time.Duration(*opts.TimeoutSeconds) * time.Second
	}
	result = &v1alpha1.AnalysisRunList{}
	err = c.client.Get().
		Namespace(c.ns).
		Resource("analysisruns").
		VersionedParams(&opts, scheme.ParameterCodec).
		Timeout(timeout).
		Do(ctx).
		Into(result)
	return
}
```

---

</SwmSnippet>

## Watch

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="97:2:2" line-data="// Watch returns a watch.Interface that watches the requested analysisRuns.">`Watch`</SwmToken> function returns a <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="97:8:10" line-data="// Watch returns a watch.Interface that watches the requested analysisRuns.">`watch.Interface`</SwmToken> that watches the requested <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="59:8:8" line-data="// newAnalysisRuns returns a AnalysisRuns">`AnalysisRuns`</SwmToken>.

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" line="97">

---

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="97:2:2" line-data="// Watch returns a watch.Interface that watches the requested analysisRuns.">`Watch`</SwmToken> function sends a GET request with watch parameters to watch the requested <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="59:8:8" line-data="// newAnalysisRuns returns a AnalysisRuns">`AnalysisRuns`</SwmToken> and returns a <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="97:8:10" line-data="// Watch returns a watch.Interface that watches the requested analysisRuns.">`watch.Interface`</SwmToken>.

```go
// Watch returns a watch.Interface that watches the requested analysisRuns.
func (c *analysisRuns) Watch(ctx context.Context, opts v1.ListOptions) (watch.Interface, error) {
	var timeout time.Duration
	if opts.TimeoutSeconds != nil {
		timeout = time.Duration(*opts.TimeoutSeconds) * time.Second
	}
	opts.Watch = true
	return c.client.Get().
		Namespace(c.ns).
		Resource("analysisruns").
		VersionedParams(&opts, scheme.ParameterCodec).
		Timeout(timeout).
		Watch(ctx)
}
```

---

</SwmSnippet>

## Patch

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="182:2:2" line-data="// Patch applies the patch and returns the patched analysisRun.">`Patch`</SwmToken> function applies the patch and returns the patched <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="68:36:36" line-data="func (c *analysisRuns) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken>.

<SwmSnippet path="/pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" line="182">

---

The <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="182:2:2" line-data="// Patch applies the patch and returns the patched analysisRun.">`Patch`</SwmToken> function sends a PATCH request to apply changes to an <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="183:56:56" line-data="func (c *analysisRuns) Patch(ctx context.Context, name string, pt types.PatchType, data []byte, opts v1.PatchOptions, subresources ...string) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken> and returns the patched <SwmToken path="pkg/client/clientset/versioned/typed/rollouts/v1alpha1/analysisrun.go" pos="183:56:56" line-data="func (c *analysisRuns) Patch(ctx context.Context, name string, pt types.PatchType, data []byte, opts v1.PatchOptions, subresources ...string) (result *v1alpha1.AnalysisRun, err error) {">`AnalysisRun`</SwmToken>.

```go
// Patch applies the patch and returns the patched analysisRun.
func (c *analysisRuns) Patch(ctx context.Context, name string, pt types.PatchType, data []byte, opts v1.PatchOptions, subresources ...string) (result *v1alpha1.AnalysisRun, err error) {
	result = &v1alpha1.AnalysisRun{}
	err = c.client.Patch(pt).
		Namespace(c.ns).
		Resource("analysisruns").
		Name(name).
		SubResource(subresources...).
		VersionedParams(&opts, scheme.ParameterCodec).
		Body(data).
		Do(ctx).
		Into(result)
	return
}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
