---
title: Get Rollout Details
---
# Overview

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="42:5:5" line-data="		Short:        &quot;Get details about a rollout&quot;,">`Get`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:21:21" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`rollout`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="42:7:7" line-data="		Short:        &quot;Get details about a rollout&quot;,">`details`</SwmToken> command is used to retrieve detailed information about a specific rollout in a Kubernetes cluster managed by Argo Rollouts. This command provides insights into the status, strategy, and other critical details of the rollout.

# Basic Usage

To get details about a specific rollout, use the command <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="15:14:14" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/kubectl-argo-rollouts/cmd/signals&quot;">`kubectl`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="14:8:8" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/apiclient/rollout&quot;">`argo`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:17:17" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`rollouts`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:19:19" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`get`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:21:21" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`rollout`</SwmToken>` <rollout-name>`. For example, to get details about a rollout named 'guestbook', you would use:

<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="15:14:14" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/kubectl-argo-rollouts/cmd/signals&quot;">`kubectl`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="14:8:8" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/apiclient/rollout&quot;">`argo`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:17:17" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`rollouts`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:19:19" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`get`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:21:21" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`rollout`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="25:11:11" line-data="	%[1]s get rollout guestbook">`guestbook`</SwmToken>

# Watching Rollout Progress

You can watch the progress of a rollout in real-time by adding the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="28:13:14" line-data="  	%[1]s get rollout guestbook -w">`-w`</SwmToken> flag to the command. This will continuously update the rollout status. For example:

<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="15:14:14" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/kubectl-argo-rollouts/cmd/signals&quot;">`kubectl`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="14:8:8" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/apiclient/rollout&quot;">`argo`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:17:17" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`rollouts`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:19:19" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`get`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:21:21" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`rollout`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="25:11:11" line-data="	%[1]s get rollout guestbook">`guestbook`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="28:13:14" line-data="  	%[1]s get rollout guestbook -w">`-w`</SwmToken>

# Watching Rollout with Timeout

To watch the rollout and fail if it takes more than a specified time, use the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="31:16:19" line-data="	%[1]s get rollout guestbook -w --timeout-seconds 60`">`--timeout-seconds`</SwmToken> option. For example, to watch the rollout and fail if it takes more than 60 seconds:

<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="15:14:14" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/kubectl-argo-rollouts/cmd/signals&quot;">`kubectl`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="14:8:8" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/apiclient/rollout&quot;">`argo`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:17:17" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`rollouts`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:19:19" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`get`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:21:21" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`rollout`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="25:11:11" line-data="	%[1]s get rollout guestbook">`guestbook`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="28:13:14" line-data="  	%[1]s get rollout guestbook -w">`-w`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="31:16:19" line-data="	%[1]s get rollout guestbook -w --timeout-seconds 60`">`--timeout-seconds`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="30:22:22" line-data="	# Watch the rollout, fail if it takes more than 60 seconds">`60`</SwmToken>

# Main Functions

Several main functions are involved in the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="42:5:5" line-data="		Short:        &quot;Get details about a rollout&quot;,">`Get`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:21:21" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`rollout`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="42:7:7" line-data="		Short:        &quot;Get details about a rollout&quot;,">`details`</SwmToken> command. These include <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:2:2" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`NewCmdGetRollout`</SwmToken>, <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="81:5:5" line-data="				go getOptions.WatchRollout(stopCh, rolloutUpdates)">`WatchRollout`</SwmToken>, and <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="140:9:9" line-data="func (o *GetOptions) PrintRollout(roInfo *rollout.RolloutInfo) {">`PrintRollout`</SwmToken>.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" line="34">

---

## <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:2:2" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`NewCmdGetRollout`</SwmToken>

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:2:2" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`NewCmdGetRollout`</SwmToken> function returns a new instance of the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="34:17:21" line-data="// NewCmdGetRollout returns a new instance of an `rollouts get rollout` command">`rollouts get rollout`</SwmToken> command. It sets up the command with necessary flags and handlers to get details about a rollout.

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

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" line="140">

---

## <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="140:9:9" line-data="func (o *GetOptions) PrintRollout(roInfo *rollout.RolloutInfo) {">`PrintRollout`</SwmToken>

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/get/get_rollout.go" pos="140:9:9" line-data="func (o *GetOptions) PrintRollout(roInfo *rollout.RolloutInfo) {">`PrintRollout`</SwmToken> function prints detailed information about the rollout, including its status, strategy, images, and replicas.

```go
func (o *GetOptions) PrintRollout(roInfo *rollout.RolloutInfo) {
	fmt.Fprintf(o.Out, tableFormat, "Name:", roInfo.ObjectMeta.Name)
	fmt.Fprintf(o.Out, tableFormat, "Namespace:", roInfo.ObjectMeta.Namespace)
	fmt.Fprintf(o.Out, tableFormat, "Status:", o.colorize(roInfo.Icon)+" "+roInfo.Status)
	if roInfo.Message != "" {
		fmt.Fprintf(o.Out, tableFormat, "Message:", roInfo.Message)
	}
	fmt.Fprintf(o.Out, tableFormat, "Strategy:", roInfo.Strategy)
	if roInfo.Strategy == "Canary" {
		fmt.Fprintf(o.Out, tableFormat, "  Step:", roInfo.Step)
		fmt.Fprintf(o.Out, tableFormat, "  SetWeight:", roInfo.SetWeight)
		fmt.Fprintf(o.Out, tableFormat, "  ActualWeight:", roInfo.ActualWeight)
	}
	images := info.Images(roInfo)
	if len(images) > 0 {
		fmt.Fprintf(o.Out, tableFormat, "Images:", o.formatImage(images[0]))
		for i := 1; i < len(images); i++ {
			fmt.Fprintf(o.Out, tableFormat, "", o.formatImage(images[i]))
		}
	}
	fmt.Fprint(o.Out, "Replicas:\n")
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
