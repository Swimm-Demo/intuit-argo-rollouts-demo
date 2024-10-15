---
title: Basic Concepts of Lint Command
---
# Basic Concepts of Lint Command

Lint refers to the process of analyzing and validating a Rollout resource from a file. This ensures that the resource adheres to the expected structure and rules.

## Lint Command Usage

The command <SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="12:14:14" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/kubectl-argo-rollouts/options&quot;">`kubectl`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="9:8:8" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/apis/rollouts&quot;">`argo`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="40:17:17" line-data="// NewCmdLint returns a new instance of a `rollouts lint` command">`rollouts`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="40:19:19" line-data="// NewCmdLint returns a new instance of a `rollouts lint` command">`lint`</SwmToken> is used to perform this linting and validation. For example, you can use <SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="12:14:14" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/kubectl-argo-rollouts/options&quot;">`kubectl`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="9:8:8" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/apis/rollouts&quot;">`argo`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="40:17:17" line-data="// NewCmdLint returns a new instance of a `rollouts lint` command">`rollouts`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="40:19:19" line-data="// NewCmdLint returns a new instance of a `rollouts lint` command">`lint`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="37:9:10" line-data="	%[1]s lint -f my-rollout.yaml`">`-f`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="37:12:16" line-data="	%[1]s lint -f my-rollout.yaml`">`my-rollout.yaml`</SwmToken> to lint a specific Rollout resource file.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/lint/lint.go" line="24">

---

## <SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="24:2:2" line-data="type LintOptions struct {">`LintOptions`</SwmToken> Struct

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="24:2:2" line-data="type LintOptions struct {">`LintOptions`</SwmToken> struct holds the options for the lint command, including the file to be linted.

```go
type LintOptions struct {
	options.ArgoRolloutsOptions
	File string
}
```

---

</SwmSnippet>

## <SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="40:2:2" line-data="// NewCmdLint returns a new instance of a `rollouts lint` command">`NewCmdLint`</SwmToken> Function

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="40:2:2" line-data="// NewCmdLint returns a new instance of a `rollouts lint` command">`NewCmdLint`</SwmToken> function creates a new instance of the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="40:17:19" line-data="// NewCmdLint returns a new instance of a `rollouts lint` command">`rollouts lint`</SwmToken> command. It sets up the command's usage, description, and execution logic. This function is essential for initializing the linting process.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/lint/lint.go" line="40">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="40:2:2" line-data="// NewCmdLint returns a new instance of a `rollouts lint` command">`NewCmdLint`</SwmToken> function sets up the command's usage, description, and execution logic. It also defines the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="51:1:1" line-data="		RunE: func(c *cobra.Command, args []string) error {">`RunE`</SwmToken> function which executes the linting process.

```go
// NewCmdLint returns a new instance of a `rollouts lint` command
func NewCmdLint(o *options.ArgoRolloutsOptions) *cobra.Command {
	lintOptions := LintOptions{
		ArgoRolloutsOptions: *o,
	}
	var cmd = &cobra.Command{
		Use:          "lint",
		Short:        "Lint and validate a Rollout",
		Long:         "This command lints and validates a new Rollout resource from a file.",
		Example:      o.Example(lintExample),
		SilenceUsage: true,
		RunE: func(c *cobra.Command, args []string) error {
			if lintOptions.File == "" {
				return o.UsageErr(c)
			}

			return lintOptions.lintResource(lintOptions.File)
		},
	}
	cmd.Flags().StringVarP(&lintOptions.File, "filename", "f", "", "File to lint")
	return cmd
```

---

</SwmSnippet>

## <SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="56:5:5" line-data="			return lintOptions.lintResource(lintOptions.File)">`lintResource`</SwmToken> Method

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/lint/lint.go" pos="56:5:5" line-data="			return lintOptions.lintResource(lintOptions.File)">`lintResource`</SwmToken> method reads the specified file, decodes its content, and performs validation checks. It ensures that the Rollout resource adheres to the expected structure and references.

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
