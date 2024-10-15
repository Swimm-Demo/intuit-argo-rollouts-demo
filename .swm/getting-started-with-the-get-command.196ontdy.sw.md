---
title: Getting Started with the Get Command
---
# Introduction

<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="73:3:3" line-data="	# Get a rollout">`Get`</SwmToken> is a command used to retrieve details about rollouts and experiments in the Argo Rollouts framework. This document will guide you through the initialization, usage, and customization of the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="1:2:2" line-data="package get">`get`</SwmToken> command.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/get/get.go" line="1">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="1:2:2" line-data="package get">`get`</SwmToken> package is imported and initialized here to set up the Get command.

```go
package get

import (
	"fmt"
	"io"
```

---

</SwmSnippet>

# <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="99:2:2" line-data="type GetOptions struct {">`GetOptions`</SwmToken> Type

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="99:2:2" line-data="type GetOptions struct {">`GetOptions`</SwmToken> type defines various options for the Get command, such as <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="100:1:1" line-data="	Watch          bool">`Watch`</SwmToken>, <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="101:1:1" line-data="	NoColor        bool">`NoColor`</SwmToken>, and <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="102:1:1" line-data="	TimeoutSeconds int">`TimeoutSeconds`</SwmToken>. These options allow you to customize the behavior of the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="1:2:2" line-data="package get">`get`</SwmToken> command.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/get/get.go" line="99">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="99:2:2" line-data="type GetOptions struct {">`GetOptions`</SwmToken> struct defines the options available for the Get command.

```go
type GetOptions struct {
	Watch          bool
	NoColor        bool
	TimeoutSeconds int

	options.ArgoRolloutsOptions
}
```

---

</SwmSnippet>

# Get Rollout Example

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="72:1:1" line-data="	getExample = `">`getExample`</SwmToken> constant provides an example of how to use the Get command to retrieve a rollout. This example demonstrates the basic usage of the command.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/get/get.go" line="71">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="72:1:1" line-data="	getExample = `">`getExample`</SwmToken> constant provides an example of how to use the Get command to retrieve a rollout.

```go
const (
	getExample = `
	# Get a rollout
	%[1]s get rollout guestbook
```

---

</SwmSnippet>

# Get Usage Information

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="82:1:1" line-data="	getUsage = `This command consists of multiple subcommands which can be used to get extended information about a rollout or experiment.`">`getUsage`</SwmToken> and <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="84:1:1" line-data="	getUsageCommon = `It returns a bunch of metadata on a resource and a tree view of the child resources created by the parent.">`getUsageCommon`</SwmToken> constants describe the usage of the Get command and its subcommands. These constants provide detailed information on how to use the command and what to expect from its output.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/get/get.go" line="80">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="82:1:1" line-data="	getUsage = `This command consists of multiple subcommands which can be used to get extended information about a rollout or experiment.`">`getUsage`</SwmToken> and <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="84:1:1" line-data="	getUsageCommon = `It returns a bunch of metadata on a resource and a tree view of the child resources created by the parent.">`getUsageCommon`</SwmToken> constants describe the usage of the Get command and its subcommands.

```go
	%[1]s get experiment my-experiment`

	getUsage = `This command consists of multiple subcommands which can be used to get extended information about a rollout or experiment.`

	getUsageCommon = `It returns a bunch of metadata on a resource and a tree view of the child resources created by the parent.
	
Tree view icons
```

---

</SwmSnippet>

# Clear Method

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="132:2:2" line-data="// Clear clears the terminal for updates for live watching of objects">`Clear`</SwmToken> method is used to clear the terminal for updates when live watching objects. This is particularly useful for keeping the terminal output clean and readable.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/get/get.go" line="132">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="132:2:2" line-data="// Clear clears the terminal for updates for live watching of objects">`Clear`</SwmToken> method clears the terminal for updates when live watching objects.

```go
// Clear clears the terminal for updates for live watching of objects
func (o *GetOptions) Clear() {
	fmt.Fprint(o.Out, "\033[H\033[2J")
	fmt.Fprint(o.Out, "\033[0;0H")
}
```

---

</SwmSnippet>

# Get Endpoints

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get.go" pos="1:2:2" line-data="package get">`get`</SwmToken> command integrates with view controllers to provide detailed and visual representations of rollouts and experiments. This section covers the specific endpoints for rollouts and experiments.

## <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:2:2" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`NewCmdGetRollout`</SwmToken>

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:2:2" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`NewCmdGetRollout`</SwmToken> function returns a new instance of the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:17:21" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`rollouts get rollout`</SwmToken> command. This command is used to get details about a specific rollout, including its status, strategy, and associated images. It supports watching live updates to the rollout and can be customized with flags such as `--watch`, `--no-color`, and <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="31:16:19" line-data="	%[1]s get rollout guestbook -w --timeout-seconds 60`">`--timeout-seconds`</SwmToken>.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" line="34">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:2:2" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`NewCmdGetRollout`</SwmToken> function returns a new instance of the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:17:21" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`rollouts get rollout`</SwmToken> command.

```go
// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command
func NewCmdGetRollout(o *options.ArgoRolloutsOptions) *cobra.Command {
	getOptions := GetOptions{
		ArgoRolloutsOptions: *o,
	}

	var cmd = &cobra.Command{
		Use:          "rollout ROLLOUT_NAME",
		Short:        "Get details about a rollout",
		Long:         "Get details about and visual representation of a rollout. " + getUsageCommon,
		Aliases:      []string{"ro", "rollouts"},
		Example:      o.Example(getRolloutExample),
		SilenceUsage: true,
		RunE: func(c *cobra.Command, args []string) error {
			if len(args) != 1 {
				return o.UsageErr(c)
			}
			name := args[0]
			controller := viewcontroller.NewRolloutViewController(o.Namespace(), name, getOptions.KubeClientset(), getOptions.RolloutsClientset())
			ctx, cancel := context.WithCancel(context.Background())
			defer cancel()
```

---

</SwmSnippet>

## <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_experiment.go" pos="29:2:2" line-data="// NewCmdGetExperiment returns a new instance of an `rollouts get experiment` command">`NewCmdGetExperiment`</SwmToken>

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_experiment.go" pos="29:2:2" line-data="// NewCmdGetExperiment returns a new instance of an `rollouts get experiment` command">`NewCmdGetExperiment`</SwmToken> function returns a new instance of the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_experiment.go" pos="29:17:21" line-data="// NewCmdGetExperiment returns a new instance of an `rollouts get experiment` command">`rollouts get experiment`</SwmToken> command. This command is used to get details about a specific experiment, including its status and associated images. It supports watching live updates to the experiment and can be customized with flags such as `--watch` and `--no-color`.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/get/get_experiment.go" line="29">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_experiment.go" pos="29:2:2" line-data="// NewCmdGetExperiment returns a new instance of an `rollouts get experiment` command">`NewCmdGetExperiment`</SwmToken> function returns a new instance of the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_experiment.go" pos="29:17:21" line-data="// NewCmdGetExperiment returns a new instance of an `rollouts get experiment` command">`rollouts get experiment`</SwmToken> command.

```go
// NewCmdGetExperiment returns a new instance of an `rollouts get experiment` command
func NewCmdGetExperiment(o *options.ArgoRolloutsOptions) *cobra.Command {
	getOptions := GetOptions{
		ArgoRolloutsOptions: *o,
	}

	var cmd = &cobra.Command{
		Use:          "experiment EXPERIMENT_NAME",
		Aliases:      []string{"exp", "experiments"},
		Short:        "Get details about an Experiment",
		Long:         "Get details about and visual representation of a experiment. " + getUsageCommon,
		Example:      o.Example(experimentExample),
		SilenceUsage: true,
		RunE: func(c *cobra.Command, args []string) error {
			if len(args) != 1 {
				return o.UsageErr(c)
			}
			name := args[0]
			controller := viewcontroller.NewExperimentViewController(o.Namespace(), name, getOptions.KubeClientset(), getOptions.RolloutsClientset())
			ctx := context.Background()
			controller.Start(ctx)
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
