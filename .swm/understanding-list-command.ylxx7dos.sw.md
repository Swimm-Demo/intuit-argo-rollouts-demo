---
title: Understanding List Command
---
# Understanding List Command

The `list` command in `Cmd` is used to list all rollouts or experiments within a specified namespace. If no namespace is specified, it uses the current namespace context. The command has multiple subcommands, such as <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list_rollouts.go" pos="34:19:21" line-data="// NewCmdListRollouts returns a new instance of an `rollouts list rollouts` command">`list rollouts`</SwmToken> and <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list_experiments.go" pos="31:19:21" line-data="// NewCmdListExperiments returns a new instance of an `rollouts list experiments` command">`list experiments`</SwmToken>, to provide specific listings.

## Initialization

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list.go" pos="34:2:2" line-data="// NewCmdList returns a new instance of an `rollouts list` command">`NewCmdList`</SwmToken> function initializes the `list` command and adds the subcommands for rollouts and experiments. This function sets up the command structure and ensures that the appropriate subcommands are available.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/list/list.go" line="34">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list.go" pos="34:2:2" line-data="// NewCmdList returns a new instance of an `rollouts list` command">`NewCmdList`</SwmToken> function initializes the `list` command and adds the subcommands for rollouts and experiments.

```go
// NewCmdList returns a new instance of an `rollouts list` command
func NewCmdList(o *options.ArgoRolloutsOptions) *cobra.Command {
	var cmd = &cobra.Command{
		Use:          "list <rollout|experiment>",
```

---

</SwmSnippet>

### <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list.go" pos="13:2:2" line-data="type ListOptions struct {">`ListOptions`</SwmToken> Struct

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list.go" pos="13:2:2" line-data="type ListOptions struct {">`ListOptions`</SwmToken> struct defines the options available for the `list` command, including fields like <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list.go" pos="14:1:1" line-data="	name          string">`name`</SwmToken>, <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list.go" pos="15:1:1" line-data="	allNamespaces bool">`allNamespaces`</SwmToken>, <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list.go" pos="16:1:1" line-data="	watch         bool">`watch`</SwmToken>, and <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list.go" pos="17:1:1" line-data="	timestamps    bool">`timestamps`</SwmToken>. These fields provide flexibility in how the command is executed.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/list/list.go" line="13">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list.go" pos="13:2:2" line-data="type ListOptions struct {">`ListOptions`</SwmToken> struct defines the options available for the `list` command.

```go
type ListOptions struct {
	name          string
	allNamespaces bool
	watch         bool
	timestamps    bool

	options.ArgoRolloutsOptions
}
```

---

</SwmSnippet>

## List Rollouts

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list_rollouts.go" pos="34:19:21" line-data="// NewCmdListRollouts returns a new instance of an `rollouts list rollouts` command">`list rollouts`</SwmToken> endpoint is used to list all rollouts within a specified namespace. If no namespace is specified, it uses the current namespace context. The command can be customized with various flags such as <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list_rollouts.go" pos="23:11:12" line-data="	%[1]s list rollouts --name my-rollout">`--name`</SwmToken> to filter by rollout name, <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list_rollouts.go" pos="26:11:14" line-data="	%[1]s list rollouts --all-namespaces">`--all-namespaces`</SwmToken> to include all namespaces, and <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list_rollouts.go" pos="29:11:12" line-data="	%[1]s list rollouts --watch`">`--watch`</SwmToken> to watch for changes.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/list/list_rollouts.go" line="34">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list_rollouts.go" pos="34:19:21" line-data="// NewCmdListRollouts returns a new instance of an `rollouts list rollouts` command">`list rollouts`</SwmToken> endpoint is used to list all rollouts within a specified namespace.

```go
// NewCmdListRollouts returns a new instance of an `rollouts list rollouts` command
func NewCmdListRollouts(o *options.ArgoRolloutsOptions) *cobra.Command {
	listOptions := ListOptions{
		ArgoRolloutsOptions: *o,
	}

	var cmd = &cobra.Command{
		Use:          "rollouts",
		Short:        "List rollouts",
		Long:         listRolloutsUsage,
		Aliases:      []string{"ro", "rollout"},
		Example:      o.Example(listRolloutsExample),
		SilenceUsage: true,
		RunE: func(c *cobra.Command, args []string) error {
			ctx := c.Context()
			var namespace string
			if listOptions.allNamespaces {
				namespace = metav1.NamespaceAll
			} else {
				namespace = o.Namespace()
			}
```

---

</SwmSnippet>

## List Experiments

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list_experiments.go" pos="31:19:21" line-data="// NewCmdListExperiments returns a new instance of an `rollouts list experiments` command">`list experiments`</SwmToken> endpoint is used to list all experiments within a specified namespace. Similar to <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list_rollouts.go" pos="34:19:21" line-data="// NewCmdListRollouts returns a new instance of an `rollouts list rollouts` command">`list rollouts`</SwmToken>, if no namespace is specified, it uses the current namespace context. The command can be customized with the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list_rollouts.go" pos="26:11:14" line-data="	%[1]s list rollouts --all-namespaces">`--all-namespaces`</SwmToken> flag to include all namespaces.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/list/list_experiments.go" line="31">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list_experiments.go" pos="31:19:21" line-data="// NewCmdListExperiments returns a new instance of an `rollouts list experiments` command">`list experiments`</SwmToken> endpoint is used to list all experiments within a specified namespace.

```go
// NewCmdListExperiments returns a new instance of an `rollouts list experiments` command
func NewCmdListExperiments(o *options.ArgoRolloutsOptions) *cobra.Command {
	listOptions := ListOptions{
		ArgoRolloutsOptions: *o,
	}

	var cmd = &cobra.Command{
		Use:          "experiments",
		Short:        "List experiments",
		Long:         listExperimentsUsage,
		Example:      o.Example(listExperimentsExample),
		Aliases:      []string{"exp", "experiment"},
		SilenceUsage: true,
		RunE: func(c *cobra.Command, args []string) error {
			ctx := c.Context()
			var namespace string
			if listOptions.allNamespaces {
				namespace = metav1.NamespaceAll
			} else {
				namespace = o.Namespace()
			}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
