---
title: Introduction to Informers in Client Library
---
# Introduction to Informers

Informers are used to provide a shared cache of Kubernetes resources, which can be queried and watched for changes. They help reduce memory footprint and the number of connections to the server by sharing a single cache among multiple clients.

# <SwmToken path="pkg/client/informers/externalversions/internalinterfaces/factory_interfaces.go" pos="34:2:2" line-data="type SharedInformerFactory interface {">`SharedInformerFactory`</SwmToken>

The <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="38:2:2" line-data="type sharedInformerFactory struct {">`sharedInformerFactory`</SwmToken> struct holds the configuration and state for creating and managing informers. It includes fields for the client, namespace, resync periods, and maps to track informers and their states.

<SwmSnippet path="/pkg/client/informers/externalversions/factory.go" line="38">

---

The <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="38:2:2" line-data="type sharedInformerFactory struct {">`sharedInformerFactory`</SwmToken> struct is defined here. It includes fields such as <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="39:1:1" line-data="	client           versioned.Interface">`client`</SwmToken>, <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="40:1:1" line-data="	namespace        string">`namespace`</SwmToken>, <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="41:1:1" line-data="	tweakListOptions internalinterfaces.TweakListOptionsFunc">`tweakListOptions`</SwmToken>, <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="42:1:1" line-data="	lock             sync.Mutex">`lock`</SwmToken>, <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="43:1:1" line-data="	defaultResync    time.Duration">`defaultResync`</SwmToken>, <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="44:1:1" line-data="	customResync     map[reflect.Type]time.Duration">`customResync`</SwmToken>, <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="45:1:1" line-data="	transform        cache.TransformFunc">`transform`</SwmToken>, <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="47:1:1" line-data="	informers map[reflect.Type]cache.SharedIndexInformer">`informers`</SwmToken>, <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="48:3:3" line-data="	// startedInformers is used for tracking which informers have been started.">`startedInformers`</SwmToken>, <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="51:3:3" line-data="	// wg tracks how many goroutines were started.">`wg`</SwmToken>, and <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="53:3:3" line-data="	// shuttingDown is true when Shutdown has been called. It may still be running">`shuttingDown`</SwmToken>.

```go
type sharedInformerFactory struct {
	client           versioned.Interface
	namespace        string
	tweakListOptions internalinterfaces.TweakListOptionsFunc
	lock             sync.Mutex
	defaultResync    time.Duration
	customResync     map[reflect.Type]time.Duration
	transform        cache.TransformFunc

	informers map[reflect.Type]cache.SharedIndexInformer
	// startedInformers is used for tracking which informers have been started.
	// This allows Start() to be called multiple times safely.
	startedInformers map[reflect.Type]bool
	// wg tracks how many goroutines were started.
	wg sync.WaitGroup
	// shuttingDown is true when Shutdown has been called. It may still be running
	// because it needs to wait for goroutines.
	shuttingDown bool
}
```

---

</SwmSnippet>

# <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="178:2:2" line-data="// InformerFor returns the SharedIndexInformer for obj using an internal">`InformerFor`</SwmToken> Method

The <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="178:2:2" line-data="// InformerFor returns the SharedIndexInformer for obj using an internal">`InformerFor`</SwmToken> method in the <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="38:2:2" line-data="type sharedInformerFactory struct {">`sharedInformerFactory`</SwmToken> creates and returns a <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="47:11:11" line-data="	informers map[reflect.Type]cache.SharedIndexInformer">`SharedIndexInformer`</SwmToken> for a given Kubernetes resource. It ensures that only one informer exists for each resource type and manages the lifecycle of the informers.

<SwmSnippet path="/pkg/client/informers/externalversions/factory.go" line="178">

---

The <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="178:2:2" line-data="// InformerFor returns the SharedIndexInformer for obj using an internal">`InformerFor`</SwmToken> method locks the factory, checks if an informer for the given resource type already exists, and returns it if found. If the informer does not exist, <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="178:2:2" line-data="// InformerFor returns the SharedIndexInformer for obj using an internal">`InformerFor`</SwmToken> creates a new one using the provided <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="180:18:18" line-data="func (f *sharedInformerFactory) InformerFor(obj runtime.Object, newFunc internalinterfaces.NewInformerFunc) cache.SharedIndexInformer {">`newFunc`</SwmToken>, sets a transform function, stores it in the factory, and then returns it.

```go
// InformerFor returns the SharedIndexInformer for obj using an internal
// client.
func (f *sharedInformerFactory) InformerFor(obj runtime.Object, newFunc internalinterfaces.NewInformerFunc) cache.SharedIndexInformer {
	f.lock.Lock()
	defer f.lock.Unlock()

	informerType := reflect.TypeOf(obj)
	informer, exists := f.informers[informerType]
	if exists {
		return informer
	}

	resyncPeriod, exists := f.customResync[informerType]
	if !exists {
		resyncPeriod = f.defaultResync
	}

	informer = newFunc(f.client, resyncPeriod)
	informer.SetTransform(f.transform)
	f.informers[informerType] = informer
```

---

</SwmSnippet>

# <SwmToken path="pkg/client/informers/externalversions/rollouts/v1alpha1/analysisrun.go" pos="48:2:2" line-data="// NewAnalysisRunInformer constructs a new informer for AnalysisRun type.">`NewAnalysisRunInformer`</SwmToken>

The <SwmToken path="pkg/client/informers/externalversions/rollouts/v1alpha1/analysisrun.go" pos="48:2:2" line-data="// NewAnalysisRunInformer constructs a new informer for AnalysisRun type.">`NewAnalysisRunInformer`</SwmToken> function constructs a new informer for the <SwmToken path="pkg/client/informers/externalversions/rollouts/v1alpha1/analysisrun.go" pos="48:14:14" line-data="// NewAnalysisRunInformer constructs a new informer for AnalysisRun type.">`AnalysisRun`</SwmToken> type. It calls <SwmToken path="pkg/client/informers/externalversions/rollouts/v1alpha1/analysisrun.go" pos="52:3:3" line-data="	return NewFilteredAnalysisRunInformer(client, namespace, resyncPeriod, indexers, nil)">`NewFilteredAnalysisRunInformer`</SwmToken> to create the informer with specific parameters.

<SwmSnippet path="/pkg/client/informers/externalversions/rollouts/v1alpha1/analysisrun.go" line="48">

---

The <SwmToken path="pkg/client/informers/externalversions/rollouts/v1alpha1/analysisrun.go" pos="48:2:2" line-data="// NewAnalysisRunInformer constructs a new informer for AnalysisRun type.">`NewAnalysisRunInformer`</SwmToken> function constructs a new informer for the <SwmToken path="pkg/client/informers/externalversions/rollouts/v1alpha1/analysisrun.go" pos="48:14:14" line-data="// NewAnalysisRunInformer constructs a new informer for AnalysisRun type.">`AnalysisRun`</SwmToken> type. It calls <SwmToken path="pkg/client/informers/externalversions/rollouts/v1alpha1/analysisrun.go" pos="52:3:3" line-data="	return NewFilteredAnalysisRunInformer(client, namespace, resyncPeriod, indexers, nil)">`NewFilteredAnalysisRunInformer`</SwmToken> to create the informer with specific parameters.

```go
// NewAnalysisRunInformer constructs a new informer for AnalysisRun type.
// Always prefer using an informer factory to get a shared informer instead of getting an independent
// one. This reduces memory footprint and number of connections to the server.
func NewAnalysisRunInformer(client versioned.Interface, namespace string, resyncPeriod time.Duration, indexers cache.Indexers) cache.SharedIndexInformer {
	return NewFilteredAnalysisRunInformer(client, namespace, resyncPeriod, indexers, nil)
}
```

---

</SwmSnippet>

# <SwmToken path="pkg/client/informers/externalversions/rollouts/v1alpha1/analysisrun.go" pos="52:3:3" line-data="	return NewFilteredAnalysisRunInformer(client, namespace, resyncPeriod, indexers, nil)">`NewFilteredAnalysisRunInformer`</SwmToken>

The <SwmToken path="pkg/client/informers/externalversions/rollouts/v1alpha1/analysisrun.go" pos="52:3:3" line-data="	return NewFilteredAnalysisRunInformer(client, namespace, resyncPeriod, indexers, nil)">`NewFilteredAnalysisRunInformer`</SwmToken> function constructs a new informer for the <SwmToken path="pkg/client/informers/externalversions/rollouts/v1alpha1/analysisrun.go" pos="48:14:14" line-data="// NewAnalysisRunInformer constructs a new informer for AnalysisRun type.">`AnalysisRun`</SwmToken> type. It sets up the list and watch functions to interact with the Kubernetes API and returns a <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="47:11:11" line-data="	informers map[reflect.Type]cache.SharedIndexInformer">`SharedIndexInformer`</SwmToken>.

<SwmSnippet path="/pkg/client/informers/externalversions/rollouts/v1alpha1/analysisrun.go" line="55">

---

The <SwmToken path="pkg/client/informers/externalversions/rollouts/v1alpha1/analysisrun.go" pos="55:2:2" line-data="// NewFilteredAnalysisRunInformer constructs a new informer for AnalysisRun type.">`NewFilteredAnalysisRunInformer`</SwmToken> function sets up the list and watch functions to interact with the Kubernetes API and returns a <SwmToken path="pkg/client/informers/externalversions/rollouts/v1alpha1/analysisrun.go" pos="58:39:39" line-data="func NewFilteredAnalysisRunInformer(client versioned.Interface, namespace string, resyncPeriod time.Duration, indexers cache.Indexers, tweakListOptions internalinterfaces.TweakListOptionsFunc) cache.SharedIndexInformer {">`SharedIndexInformer`</SwmToken>.

```go
// NewFilteredAnalysisRunInformer constructs a new informer for AnalysisRun type.
// Always prefer using an informer factory to get a shared informer instead of getting an independent
// one. This reduces memory footprint and number of connections to the server.
func NewFilteredAnalysisRunInformer(client versioned.Interface, namespace string, resyncPeriod time.Duration, indexers cache.Indexers, tweakListOptions internalinterfaces.TweakListOptionsFunc) cache.SharedIndexInformer {
	return cache.NewSharedIndexInformer(
		&cache.ListWatch{
			ListFunc: func(options v1.ListOptions) (runtime.Object, error) {
				if tweakListOptions != nil {
					tweakListOptions(&options)
				}
				return client.ArgoprojV1alpha1().AnalysisRuns(namespace).List(context.TODO(), options)
			},
			WatchFunc: func(options v1.ListOptions) (watch.Interface, error) {
				if tweakListOptions != nil {
					tweakListOptions(&options)
				}
				return client.ArgoprojV1alpha1().AnalysisRuns(namespace).Watch(context.TODO(), options)
			},
		},
		&rolloutsv1alpha1.AnalysisRun{},
		resyncPeriod,
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/informers/externalversions/generic.go" line="41">

---

The <SwmToken path="pkg/client/informers/externalversions/generic.go" pos="41:2:2" line-data="// Informer returns the SharedIndexInformer.">`Informer`</SwmToken> method in the <SwmToken path="pkg/client/informers/externalversions/generic.go" pos="42:6:6" line-data="func (f *genericInformer) Informer() cache.SharedIndexInformer {">`genericInformer`</SwmToken> struct returns the <SwmToken path="pkg/client/informers/externalversions/generic.go" pos="41:8:8" line-data="// Informer returns the SharedIndexInformer.">`SharedIndexInformer`</SwmToken> for the resource. This method is used to access the shared informer instance that is responsible for watching and caching the resource.

```go
// Informer returns the SharedIndexInformer.
func (f *genericInformer) Informer() cache.SharedIndexInformer {
	return f.informer
}
```

---

</SwmSnippet>

# <SwmToken path="pkg/client/informers/externalversions/generic.go" pos="51:2:2" line-data="// ForResource gives generic access to a shared informer of the matching type">`ForResource`</SwmToken> Method

The <SwmToken path="pkg/client/informers/externalversions/generic.go" pos="51:2:2" line-data="// ForResource gives generic access to a shared informer of the matching type">`ForResource`</SwmToken> method in the <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="38:2:2" line-data="type sharedInformerFactory struct {">`sharedInformerFactory`</SwmToken> struct provides generic access to a shared informer of the matching type. It uses a switch case to determine the resource type and returns the corresponding <SwmToken path="pkg/client/informers/externalversions/generic.go" pos="42:6:6" line-data="func (f *genericInformer) Informer() cache.SharedIndexInformer {">`genericInformer`</SwmToken> instance. If no matching informer is found, it returns an error.

<SwmSnippet path="/pkg/client/informers/externalversions/generic.go" line="51">

---

The <SwmToken path="pkg/client/informers/externalversions/generic.go" pos="51:2:2" line-data="// ForResource gives generic access to a shared informer of the matching type">`ForResource`</SwmToken> method uses a switch case to determine the resource type and returns the corresponding <SwmToken path="pkg/client/informers/externalversions/generic.go" pos="57:4:4" line-data="		return &amp;genericInformer{resource: resource.GroupResource(), informer: f.Argoproj().V1alpha1().AnalysisRuns().Informer()}, nil">`genericInformer`</SwmToken> instance. If no matching informer is found, it returns an error.

```go
// ForResource gives generic access to a shared informer of the matching type
// TODO extend this to unknown resources with a client pool
func (f *sharedInformerFactory) ForResource(resource schema.GroupVersionResource) (GenericInformer, error) {
	switch resource {
	// Group=argoproj.io, Version=v1alpha1
	case v1alpha1.SchemeGroupVersion.WithResource("analysisruns"):
		return &genericInformer{resource: resource.GroupResource(), informer: f.Argoproj().V1alpha1().AnalysisRuns().Informer()}, nil
	case v1alpha1.SchemeGroupVersion.WithResource("analysistemplates"):
		return &genericInformer{resource: resource.GroupResource(), informer: f.Argoproj().V1alpha1().AnalysisTemplates().Informer()}, nil
	case v1alpha1.SchemeGroupVersion.WithResource("clusteranalysistemplates"):
		return &genericInformer{resource: resource.GroupResource(), informer: f.Argoproj().V1alpha1().ClusterAnalysisTemplates().Informer()}, nil
	case v1alpha1.SchemeGroupVersion.WithResource("experiments"):
		return &genericInformer{resource: resource.GroupResource(), informer: f.Argoproj().V1alpha1().Experiments().Informer()}, nil
	case v1alpha1.SchemeGroupVersion.WithResource("rollouts"):
		return &genericInformer{resource: resource.GroupResource(), informer: f.Argoproj().V1alpha1().Rollouts().Informer()}, nil

	}

	return nil, fmt.Errorf("no informer found for %v", resource)
}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
