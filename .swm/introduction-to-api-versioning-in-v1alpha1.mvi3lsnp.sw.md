---
title: Introduction to API Versioning in V1alpha1
---
# Introduction

<SwmToken path="pkg/client/informers/externalversions/rollouts/interface.go" pos="29:1:1" line-data="	V1alpha1() v1alpha1.Interface">`V1alpha1`</SwmToken> is a version identifier used in the API definitions to denote the alpha version of the API. It indicates that the API is in an early testing phase and may undergo significant changes.

# <SwmToken path="pkg/apis/rollouts/v1alpha1/types.go" pos="136:1:1" line-data="	APIVersion string `json:&quot;apiVersion,omitempty&quot; protobuf:&quot;bytes,1,opt,name=apiVersion&quot;`">`APIVersion`</SwmToken> Field

The <SwmToken path="pkg/apis/rollouts/v1alpha1/types.go" pos="136:1:1" line-data="	APIVersion string `json:&quot;apiVersion,omitempty&quot; protobuf:&quot;bytes,1,opt,name=apiVersion&quot;`">`APIVersion`</SwmToken> field in the `v1alpha1.ObjectRef` struct specifies the version of the Kubernetes object being referenced. This helps in identifying the exact version of the object for operations.

# <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="616:3:3" line-data="	// ApiVersion refers to the Datadog API version being used (default: v1). v1 will eventually be deprecated.">`ApiVersion`</SwmToken> Field in <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="177:4:4" line-data="	Datadog *DatadogMetric `json:&quot;datadog,omitempty&quot; protobuf:&quot;bytes,4,opt,name=datadog&quot;`">`DatadogMetric`</SwmToken>

In the `v1alpha1.DatadogMetric` struct, the <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="616:3:3" line-data="	// ApiVersion refers to the Datadog API version being used (default: v1). v1 will eventually be deprecated.">`ApiVersion`</SwmToken> field refers to the Datadog API version being used. This field supports validation and defaulting mechanisms to ensure compatibility with different versions of the Datadog API.

<SwmSnippet path="/pkg/apis/rollouts/v1alpha1/analysis_types.go" line="529">

---

The <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="616:3:3" line-data="	// ApiVersion refers to the Datadog API version being used (default: v1). v1 will eventually be deprecated.">`ApiVersion`</SwmToken> field in the `v1alpha1.DatadogMetric` struct refers to the Datadog API version being used. This field supports validation and defaulting mechanisms to ensure compatibility with different versions of the Datadog API.

```go
type KayentaMetric struct {
	Address string `json:"address" protobuf:"bytes,1,opt,name=address"`

	Application string `json:"application" protobuf:"bytes,2,opt,name=application"`

	CanaryConfigName string `json:"canaryConfigName" protobuf:"bytes,3,opt,name=canaryConfigName"`

	MetricsAccountName       string `json:"metricsAccountName" protobuf:"bytes,4,opt,name=metricsAccountName"`
```

---

</SwmSnippet>

# Package <SwmToken path="pkg/apis/rollouts/v1alpha1/doc.go" pos="5:4:4" line-data="// Package v1alpha1 is the v1alpha1 version of the API.">`v1alpha1`</SwmToken>

The <SwmToken path="pkg/apis/rollouts/v1alpha1/doc.go" pos="5:4:4" line-data="// Package v1alpha1 is the v1alpha1 version of the API.">`v1alpha1`</SwmToken> package includes various types and structs that define the schema for different resources and their configurations. These definitions are crucial for managing rollouts and traffic routing in Kubernetes.

<SwmSnippet path="/pkg/apis/rollouts/v1alpha1/doc.go" line="1">

---

The <SwmToken path="pkg/apis/rollouts/v1alpha1/doc.go" pos="5:4:4" line-data="// Package v1alpha1 is the v1alpha1 version of the API.">`v1alpha1`</SwmToken> package includes various types and structs that define the schema for different resources and their configurations.

```go
// +k8s:deepcopy-gen=package
// +groupName=argoproj.io
// +k8s:openapi-gen=true

// Package v1alpha1 is the v1alpha1 version of the API.
package v1alpha1
```

---

</SwmSnippet>

# <SwmToken path="pkg/client/informers/externalversions/rollouts/interface.go" pos="29:1:1" line-data="	V1alpha1() v1alpha1.Interface">`V1alpha1`</SwmToken> Endpoints

The <SwmToken path="pkg/apis/rollouts/v1alpha1/experiment_types.go" pos="14:2:2" line-data="// Experiment is a specification for an Experiment resource">`Experiment`</SwmToken> struct defines the schema for an Experiment resource. It includes metadata, specifications, and status fields. The <SwmToken path="pkg/apis/rollouts/v1alpha1/experiment_types.go" pos="14:2:2" line-data="// Experiment is a specification for an Experiment resource">`Experiment`</SwmToken> resource is used to run experiments with different configurations and analyze their outcomes.

<SwmSnippet path="/pkg/apis/rollouts/v1alpha1/experiment_types.go" line="14">

---

The <SwmToken path="pkg/apis/rollouts/v1alpha1/experiment_types.go" pos="14:2:2" line-data="// Experiment is a specification for an Experiment resource">`Experiment`</SwmToken> struct defines the schema for an Experiment resource. It includes metadata, specifications, and status fields. The <SwmToken path="pkg/apis/rollouts/v1alpha1/experiment_types.go" pos="14:2:2" line-data="// Experiment is a specification for an Experiment resource">`Experiment`</SwmToken> resource is used to run experiments with different configurations and analyze their outcomes.

```go
// Experiment is a specification for an Experiment resource
// +genclient
// +k8s:deepcopy-gen:interfaces=k8s.io/apimachinery/pkg/runtime.Object
// +kubebuilder:resource:path=experiments,shortName=exp
// +kubebuilder:printcolumn:name="Status",type="string",JSONPath=".status.phase",description="Experiment status"
// +kubebuilder:printcolumn:name="Age",type="date",JSONPath=".metadata.creationTimestamp",description="Time since resource was created"
type Experiment struct {
	metav1.TypeMeta   `json:",inline"`
	metav1.ObjectMeta `json:"metadata,omitempty" protobuf:"bytes,1,opt,name=metadata"`

	Spec   ExperimentSpec   `json:"spec" protobuf:"bytes,2,opt,name=spec"`
	Status ExperimentStatus `json:"status,omitempty" protobuf:"bytes,3,opt,name=status"`
}
```

---

</SwmSnippet>

# <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="361:2:2" line-data="// AnalysisRun is an instantiation of an AnalysisTemplate">`AnalysisRun`</SwmToken>

The <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="361:2:2" line-data="// AnalysisRun is an instantiation of an AnalysisTemplate">`AnalysisRun`</SwmToken> struct defines the schema for an <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="361:2:2" line-data="// AnalysisRun is an instantiation of an AnalysisTemplate">`AnalysisRun`</SwmToken> resource. It includes metadata, specifications, and status fields. The <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="361:2:2" line-data="// AnalysisRun is an instantiation of an AnalysisTemplate">`AnalysisRun`</SwmToken> resource is used to instantiate an <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="361:14:14" line-data="// AnalysisRun is an instantiation of an AnalysisTemplate">`AnalysisTemplate`</SwmToken> and run it to analyze the performance of a rollout.

<SwmSnippet path="/pkg/apis/rollouts/v1alpha1/analysis_types.go" line="361">

---

The <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="361:2:2" line-data="// AnalysisRun is an instantiation of an AnalysisTemplate">`AnalysisRun`</SwmToken> struct defines the schema for an <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="361:2:2" line-data="// AnalysisRun is an instantiation of an AnalysisTemplate">`AnalysisRun`</SwmToken> resource. It includes metadata, specifications, and status fields. The <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="361:2:2" line-data="// AnalysisRun is an instantiation of an AnalysisTemplate">`AnalysisRun`</SwmToken> resource is used to instantiate an <SwmToken path="pkg/apis/rollouts/v1alpha1/analysis_types.go" pos="361:14:14" line-data="// AnalysisRun is an instantiation of an AnalysisTemplate">`AnalysisTemplate`</SwmToken> and run it to analyze the performance of a rollout.

```go
// AnalysisRun is an instantiation of an AnalysisTemplate
// +genclient
// +k8s:deepcopy-gen:interfaces=k8s.io/apimachinery/pkg/runtime.Object
// +kubebuilder:resource:path=analysisruns, shortName=ar
// +kubebuilder:printcolumn:name="Status",type="string",JSONPath=".status.phase",description="AnalysisRun status"
// +kubebuilder:printcolumn:name="Age",type="date",JSONPath=".metadata.creationTimestamp",description="Time since resource was created"
type AnalysisRun struct {
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
