---
title: Rollback Functionality
---
# Rollback Functionality Overview

Rollback functionality in Argo Rollouts allows users to revert to a previous rollout state if the current deployment has issues. This ensures that the deployment can quickly revert to a stable state without manual intervention.

# Using the Rollback Command

The command <SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="19:14:14" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/kubectl-argo-rollouts/options&quot;">`kubectl`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="18:8:8" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/apis/rollouts/v1alpha1&quot;">`argo`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="70:13:13" line-data="// RunUndoRollout performs the execution of &#39;rollouts undo&#39; sub command">`rollouts`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="70:15:15" line-data="// RunUndoRollout performs the execution of &#39;rollouts undo&#39; sub command">`undo`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="45:7:7" line-data="		Use:          &quot;undo ROLLOUT_NAME&quot;,">`ROLLOUT_NAME`</SwmToken> is used to perform a rollback. This command can also target specific revisions using the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="36:11:14" line-data="	%[1]s undo guestbook --to-revision=3`">`--to-revision`</SwmToken> flag.

The command <SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="19:14:14" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/kubectl-argo-rollouts/options&quot;">`kubectl`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="18:8:8" line-data="	&quot;github.com/argoproj/argo-rollouts/pkg/apis/rollouts/v1alpha1&quot;">`argo`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="70:13:13" line-data="// RunUndoRollout performs the execution of &#39;rollouts undo&#39; sub command">`rollouts`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="70:15:15" line-data="// RunUndoRollout performs the execution of &#39;rollouts undo&#39; sub command">`undo`</SwmToken>` `<SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="33:9:9" line-data="	%[1]s undo guestbook">`guestbook`</SwmToken> is an example of how to use the rollback command.

# Rollback Process

The rollback process involves identifying the desired revision and applying its configuration to the current rollout. This ensures that the deployment can quickly revert to a stable state.

# Rollback Options

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="36:11:14" line-data="	%[1]s undo guestbook --to-revision=3`">`--to-revision`</SwmToken> flag allows you to specify the revision to rollback to. By default, it rolls back to the last revision.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/undo/undo.go" line="70">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="70:2:2" line-data="// RunUndoRollout performs the execution of &#39;rollouts undo&#39; sub command">`RunUndoRollout`</SwmToken> function performs the execution of the <SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="70:13:15" line-data="// RunUndoRollout performs the execution of &#39;rollouts undo&#39; sub command">`rollouts undo`</SwmToken> sub-command. It retrieves the rollout, identifies the desired revision, and applies the configuration of that revision to the current rollout.

```go
// RunUndoRollout performs the execution of 'rollouts undo' sub command
func RunUndoRollout(rolloutIf dynamic.ResourceInterface, c kubernetes.Interface, name string, toRevision int64) (string, error) {
	ctx := context.TODO()
	var err error

	ro, err := rolloutIf.Get(ctx, name, metav1.GetOptions{})
	if err != nil {
		return "", err
	}
	rsForRevision, err := rolloutRevision(ro, c, toRevision)
	if err != nil {
		return "", err
	}

	equal, err := equalIgnoreHash(ro, rsForRevision)
	if err != nil {
		return "", err
	}
	if equal {
		return fmt.Sprintf("skipped rollback (current template already matches revision %d)", toRevision), nil
	}
```

---

</SwmSnippet>

# Handling Workload References

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="117:2:2" line-data="func undoWorkloadRef(c kubernetes.Interface, rollout *v1alpha1.Rollout, patchType types.PatchType, patch []byte) error {">`undoWorkloadRef`</SwmToken> function handles the rollback for rollouts that reference a specific workload. It applies the necessary patch to revert the workload to the specified revision.

<SwmSnippet path="/pkg/kubectl-argo-rollouts/cmd/undo/undo.go" line="117">

---

The <SwmToken path="pkg/kubectl-argo-rollouts/cmd/undo/undo.go" pos="117:2:2" line-data="func undoWorkloadRef(c kubernetes.Interface, rollout *v1alpha1.Rollout, patchType types.PatchType, patch []byte) error {">`undoWorkloadRef`</SwmToken> function handles the rollback for rollouts that reference a specific workload. It applies the necessary patch to revert the workload to the specified revision.

```go
func undoWorkloadRef(c kubernetes.Interface, rollout *v1alpha1.Rollout, patchType types.PatchType, patch []byte) error {
	var err error

	refName := rollout.Spec.WorkloadRef.Name
	namespace := rollout.GetNamespace()

	switch rollout.Spec.WorkloadRef.Kind {
	case "Deployment":
		_, err = c.AppsV1().Deployments(namespace).Patch(context.TODO(), refName, patchType, patch, metav1.PatchOptions{})
	case "ReplicaSet":
		_, err = c.AppsV1().ReplicaSets(namespace).Patch(context.TODO(), refName, patchType, patch, metav1.PatchOptions{})
	case "PodTemplate":
		_, err = c.CoreV1().PodTemplates(namespace).Patch(context.TODO(), refName, patchType, patch, metav1.PatchOptions{})
	default:
		return fmt.Errorf("workload of type %s is not supported", rollout.Spec.WorkloadRef.Kind)
	}
	return err
}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
