---
title: The AnalysisRunListerExpansion class
---
This document will cover the class <SwmToken path="pkg/client/listers/rollouts/v1alpha1/expansion_generated.go" pos="21:2:2" line-data="// AnalysisRunListerExpansion allows custom methods to be added to">`AnalysisRunListerExpansion`</SwmToken>. We will discuss:

1. What is <SwmToken path="pkg/client/listers/rollouts/v1alpha1/expansion_generated.go" pos="21:2:2" line-data="// AnalysisRunListerExpansion allows custom methods to be added to">`AnalysisRunListerExpansion`</SwmToken>
2. Variables and functions
3. Usage example

```mermaid
graph TD;
  AnalysisRunListerExpansion:::currentBaseStyle
AnalysisRunListerExpansion --> AnalysisRunLister

 classDef currentBaseStyle color:#000000,fill:#7CB9F4

%% Swimm:
%% graph TD;
%%   AnalysisRunListerExpansion:::currentBaseStyle
%% <SwmToken path="pkg/client/listers/rollouts/v1alpha1/expansion_generated.go" pos="21:2:2" line-data="// AnalysisRunListerExpansion allows custom methods to be added to">`AnalysisRunListerExpansion`</SwmToken> --> <SwmToken path="pkg/client/listers/rollouts/v1alpha1/expansion_generated.go" pos="22:2:2" line-data="// AnalysisRunLister.">`AnalysisRunLister`</SwmToken>
%% 
%%  classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is <SwmToken path="pkg/client/listers/rollouts/v1alpha1/expansion_generated.go" pos="21:2:2" line-data="// AnalysisRunListerExpansion allows custom methods to be added to">`AnalysisRunListerExpansion`</SwmToken>

The <SwmToken path="pkg/client/listers/rollouts/v1alpha1/expansion_generated.go" pos="21:2:2" line-data="// AnalysisRunListerExpansion allows custom methods to be added to">`AnalysisRunListerExpansion`</SwmToken> is an interface defined in the file <SwmPath>[pkg/client/listers/rollouts/v1alpha1/expansion_generated.go](pkg/client/listers/rollouts/v1alpha1/expansion_generated.go)</SwmPath>. It allows custom methods to be added to the <SwmToken path="pkg/client/listers/rollouts/v1alpha1/expansion_generated.go" pos="22:2:2" line-data="// AnalysisRunLister.">`AnalysisRunLister`</SwmToken>. This interface is part of the Kubernetes <SwmToken path="pkg/client/listers/rollouts/v1alpha1/analysisrun.go" pos="25:6:8" line-data="	&quot;k8s.io/client-go/tools/cache&quot;">`client-go`</SwmToken> library and is used to extend the functionality of the listers generated by the <SwmToken path="pkg/client/listers/rollouts/v1alpha1/analysisrun.go" pos="17:8:10" line-data="// Code generated by lister-gen. DO NOT EDIT.">`lister-gen`</SwmToken> tool.

<SwmSnippet path="/pkg/client/listers/rollouts/v1alpha1/expansion_generated.go" line="21">

---

# Variables and functions

The <SwmToken path="pkg/client/listers/rollouts/v1alpha1/expansion_generated.go" pos="21:2:2" line-data="// AnalysisRunListerExpansion allows custom methods to be added to">`AnalysisRunListerExpansion`</SwmToken> interface itself does not define any variables or functions. It is an empty interface that serves as a placeholder for adding custom methods to the <SwmToken path="pkg/client/listers/rollouts/v1alpha1/expansion_generated.go" pos="22:2:2" line-data="// AnalysisRunLister.">`AnalysisRunLister`</SwmToken>.

```go
// AnalysisRunListerExpansion allows custom methods to be added to
// AnalysisRunLister.
type AnalysisRunListerExpansion interface{}
```

---

</SwmSnippet>

# Usage example

To use the <SwmToken path="pkg/client/listers/rollouts/v1alpha1/expansion_generated.go" pos="21:2:2" line-data="// AnalysisRunListerExpansion allows custom methods to be added to">`AnalysisRunListerExpansion`</SwmToken>, you would typically define custom methods in a separate file that implements this interface. Here is an example of how you might extend the <SwmToken path="pkg/client/listers/rollouts/v1alpha1/expansion_generated.go" pos="22:2:2" line-data="// AnalysisRunLister.">`AnalysisRunLister`</SwmToken> with a custom method.

<SwmSnippet path="/pkg/client/listers/rollouts/v1alpha1/analysisrun.go" line="1">

---

In this example, the <SwmToken path="pkg/client/listers/rollouts/v1alpha1/expansion_generated.go" pos="22:2:2" line-data="// AnalysisRunLister.">`AnalysisRunLister`</SwmToken> is extended with a custom method `ListByNamespace`. This method would be defined in a separate file and would implement the <SwmToken path="pkg/client/listers/rollouts/v1alpha1/expansion_generated.go" pos="21:2:2" line-data="// AnalysisRunListerExpansion allows custom methods to be added to">`AnalysisRunListerExpansion`</SwmToken> interface.

```go
/*
Copyright The Kubernetes Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
*/

// Code generated by lister-gen. DO NOT EDIT.

package v1alpha1

import (
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
