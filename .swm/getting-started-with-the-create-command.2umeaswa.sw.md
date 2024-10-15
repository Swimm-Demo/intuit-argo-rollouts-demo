---
title: Getting Started with the Create Command
---
## Overview

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="52:7:7" line-data="	%[1]s create -f my-experiment.yaml -w`">`create`</SwmToken> command in Argo Rollouts is used to generate new resources such as Rollouts, Experiments, <SwmToken path="pkg/client/listers/rollouts/v1alpha1/analysistemplate.go" pos="35:1:1" line-data="	AnalysisTemplates(namespace string) AnalysisTemplateNamespaceLister">`AnalysisTemplates`</SwmToken>, <SwmToken path="pkg/apis/rollouts/validation/validation_references.go" pos="38:1:1" line-data="	ClusterAnalysisTemplates []*v1alpha1.ClusterAnalysisTemplate">`ClusterAnalysisTemplates`</SwmToken>, or <SwmToken path="pkg/client/listers/rollouts/v1alpha1/analysisrun.go" pos="35:1:1" line-data="	AnalysisRuns(namespace string) AnalysisRunNamespaceLister">`AnalysisRuns`</SwmToken>. This command can create resources from a specified file using the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="52:9:10" line-data="	%[1]s create -f my-experiment.yaml -w`">`-f`</SwmToken> flag and supports watching live updates to the resource after creation with the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="52:18:19" line-data="	%[1]s create -f my-experiment.yaml -w`">`-w`</SwmToken> flag.

## <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="68:2:2" line-data="// NewCmdCreate returns a new instance of an `rollouts create` command">`NewCmdCreate`</SwmToken> Function

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="68:2:2" line-data="// NewCmdCreate returns a new instance of an `rollouts create` command">`NewCmdCreate`</SwmToken> function is responsible for returning a new instance of the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="68:17:19" line-data="// NewCmdCreate returns a new instance of an `rollouts create` command">`rollouts create`</SwmToken> command. This command can create resources from a specified file using the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="52:9:10" line-data="	%[1]s create -f my-experiment.yaml -w`">`-f`</SwmToken> flag. It also supports watching live updates to the resource after creation with the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="52:18:19" line-data="	%[1]s create -f my-experiment.yaml -w`">`-w`</SwmToken> flag.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/create/create.go" line="68">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="68:2:2" line-data="// NewCmdCreate returns a new instance of an `rollouts create` command">`NewCmdCreate`</SwmToken> function initializes the create command, sets up the usage and example, and handles the execution logic. It ensures that the necessary files are provided and handles errors related to watching multiple resources.

```go
// NewCmdCreate returns a new instance of an `rollouts create` command
func NewCmdCreate(o *options.ArgoRolloutsOptions) *cobra.Command {
	createOptions := CreateOptions{
		ArgoRolloutsOptions: *o,
	}
	var cmd = &cobra.Command{
		Use:          "create",
		Short:        "Create a Rollout, Experiment, AnalysisTemplate, ClusterAnalysisTemplate, or AnalysisRun resource",
		Long:         "This command creates a new Rollout, Experiment, AnalysisTemplate, ClusterAnalysisTemplate, or AnalysisRun resource from a file.",
		Example:      o.Example(createExample),
		SilenceUsage: true,
		RunE: func(c *cobra.Command, args []string) error {
			createOptions.DynamicClientset()
			if len(createOptions.Files) == 0 {
				return o.UsageErr(c)
			}
			if len(createOptions.Files) > 1 && createOptions.Watch {
				return errors.New("Cannot watch multiple resources")
			}

			var objs []runtime.Object
```

---

</SwmSnippet>

## <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="154:9:9" line-data="func (c *CreateOptions) createResource(path string) (runtime.Object, error) {">`createResource`</SwmToken> Method

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="154:9:9" line-data="func (c *CreateOptions) createResource(path string) (runtime.Object, error) {">`createResource`</SwmToken> method processes each file and creates the corresponding resource. If the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="51:11:11" line-data="	# Create an experiment and watch it">`watch`</SwmToken> option is enabled, the command will monitor the created resource for updates.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/create/create.go" line="154">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="154:9:9" line-data="func (c *CreateOptions) createResource(path string) (runtime.Object, error) {">`createResource`</SwmToken> method reads the file, unmarshals the content into an unstructured object, and creates the resource using the dynamic client. It handles different resource types such as Experiments and ensures the correct namespace is used.

```go
func (c *CreateOptions) createResource(path string) (runtime.Object, error) {
	ctx := context.TODO()
	fileBytes, err := os.ReadFile(path)
	if err != nil {
		return nil, err
	}
	var un unstructured.Unstructured
	err = unmarshal(fileBytes, &un)
	if err != nil {
		return nil, err
	}
	gvk := un.GroupVersionKind()
	ns := c.getNamespace(un)
	switch {
	case gvk.Group == rollouts.Group && gvk.Kind == rollouts.ExperimentKind:
		var exp v1alpha1.Experiment
		err = unmarshal(fileBytes, &exp)
		if err != nil {
			return nil, err
		}
		obj, err := c.DynamicClient.Resource(v1alpha1.ExperimentGVR).Namespace(ns).Create(ctx, &un, metav1.CreateOptions{})
```

---

</SwmSnippet>

## Examples

To create an experiment and watch it, you can use the command: <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="68:17:17" line-data="// NewCmdCreate returns a new instance of an `rollouts create` command">`rollouts`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="52:7:7" line-data="	%[1]s create -f my-experiment.yaml -w`">`create`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="52:9:10" line-data="	%[1]s create -f my-experiment.yaml -w`">`-f`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="52:12:16" line-data="	%[1]s create -f my-experiment.yaml -w`">`my-experiment.yaml`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="52:18:19" line-data="	%[1]s create -f my-experiment.yaml -w`">`-w`</SwmToken>. This example demonstrates how to use the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="52:7:7" line-data="	%[1]s create -f my-experiment.yaml -w`">`create`</SwmToken> command with the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="52:9:10" line-data="	%[1]s create -f my-experiment.yaml -w`">`-f`</SwmToken> and <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="52:18:19" line-data="	%[1]s create -f my-experiment.yaml -w`">`-w`</SwmToken> flags.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/create/create.go" line="50">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="50:1:1" line-data="	createExample = `">`createExample`</SwmToken> constant provides an example of how to create an experiment and watch it using the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="68:17:19" line-data="// NewCmdCreate returns a new instance of an `rollouts create` command">`rollouts create`</SwmToken> command.

```go
	createExample = `
	# Create an experiment and watch it
	%[1]s create -f my-experiment.yaml -w`
```

---

</SwmSnippet>

## <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="27:2:2" line-data="type CreateOptions struct {">`CreateOptions`</SwmToken> Struct

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="27:2:2" line-data="type CreateOptions struct {">`CreateOptions`</SwmToken> struct defines the options available for the create command, including file paths and flags for specifying the source of the resource.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/create/create.go" line="27">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="27:2:2" line-data="type CreateOptions struct {">`CreateOptions`</SwmToken> struct includes fields such as <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="31:1:1" line-data="	Files    []string">`Files`</SwmToken>, `From`, <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="33:1:1" line-data="	FromFile string">`FromFile`</SwmToken>, and `Global`, which are used to configure the create command.

```go
type CreateOptions struct {
	get.GetOptions
	options.ArgoRolloutsOptions

	Files    []string
	From     string
	FromFile string
	Global   bool
}
```

---

</SwmSnippet>

## <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="233:2:2" line-data="// NewCmdCreateAnalysisRun returns a new instance of an `rollouts create analysisrun` command">`NewCmdCreateAnalysisRun`</SwmToken> Function

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="233:2:2" line-data="// NewCmdCreateAnalysisRun returns a new instance of an `rollouts create analysisrun` command">`NewCmdCreateAnalysisRun`</SwmToken> function returns a new instance of the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="233:17:21" line-data="// NewCmdCreateAnalysisRun returns a new instance of an `rollouts create analysisrun` command">`rollouts create analysisrun`</SwmToken> command. This command can create an <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="75:23:23" line-data="		Short:        &quot;Create a Rollout, Experiment, AnalysisTemplate, ClusterAnalysisTemplate, or AnalysisRun resource&quot;,">`AnalysisRun`</SwmToken> from a local <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="75:15:15" line-data="		Short:        &quot;Create a Rollout, Experiment, AnalysisTemplate, ClusterAnalysisTemplate, or AnalysisRun resource&quot;,">`AnalysisTemplate`</SwmToken> file or from a template in the cluster. It supports various flags such as <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="56:11:12" line-data="  	%[1]s create analysisrun --from-file my-analysis-template.yaml">`--from`</SwmToken>, <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="56:11:14" line-data="  	%[1]s create analysisrun --from-file my-analysis-template.yaml">`--from-file`</SwmToken>, and <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="62:11:12" line-data="  	%[1]s create analysisrun --global --from my-analysis-cluster-template.yaml">`--global`</SwmToken> to specify the source of the template.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/create/create.go" line="233">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/create/create.go" pos="233:2:2" line-data="// NewCmdCreateAnalysisRun returns a new instance of an `rollouts create analysisrun` command">`NewCmdCreateAnalysisRun`</SwmToken> function initializes the create analysisrun command, sets up the usage and example, and handles the execution logic. It ensures that the necessary templates are provided and handles errors related to multiple sources.

```go
// NewCmdCreateAnalysisRun returns a new instance of an `rollouts create analysisrun` command
func NewCmdCreateAnalysisRun(o *options.ArgoRolloutsOptions) *cobra.Command {
	createOptions := CreateAnalysisRunOptions{
		ArgoRolloutsOptions: *o,
	}
	var cmd = &cobra.Command{
		Use:          "analysisrun",
		Aliases:      []string{"ar"},
		Short:        "Create an AnalysisRun from an AnalysisTemplate or a ClusterAnalysisTemplate",
		Long:         "This command creates a new AnalysisRun from an existing AnalysisTemplate resources or from an AnalysisTemplate file.",
		Example:      o.Example(createAnalysisRunExample),
		SilenceUsage: true,
		RunE: func(c *cobra.Command, args []string) error {
			ctx := c.Context()
			createOptions.DynamicClientset()
			froms := 0
			if createOptions.From != "" {
				froms++
			}
			if createOptions.FromFile != "" {
				froms++
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
