---
title: Retrieving and Displaying Experiment Details
---
This document will cover the process of retrieving and displaying experiment details. We'll cover:

1. Initializing the command to get experiment details
2. Retrieving experiment information
3. Displaying experiment details in a user-friendly format
4. Monitoring experiment updates

Technical document: <SwmLink doc-title="Retrieving and Displaying Experiment Details">[Retrieving and Displaying Experiment Details](/.swm/retrieving-and-displaying-experiment-details.7cxd08qq.sw.md)</SwmLink>

# [Initializing the Command](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=/docs/7cxd08qq#newcmdgetexperiment)

The process begins by initializing a command to get the details of an experiment. This command is set up with necessary options and execution flow. When the command is run, it retrieves the experiment name from the user input and prepares to fetch the experiment details.

# [Retrieving Experiment Information](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=/docs/7cxd08qq#getexperimentinfo)

Once the command is initialized, it creates a controller to manage the experiment's information. The controller fetches detailed information about the experiment, including associated replica sets, pods, and analysis runs. This information is then compiled into an <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="916:2:2" line-data="type ExperimentInfo struct {">`ExperimentInfo`</SwmToken> object, which encapsulates all the relevant details about the experiment.

# [Displaying Experiment Details](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=/docs/7cxd08qq#printexperiment)

After retrieving the experiment information, the details are formatted and displayed to the user in a user-friendly format. This includes metadata, status, and associated images. The hierarchical structure of the experiment is also displayed to provide a comprehensive view of the experiment's components.

# [Monitoring Experiment Updates](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=/docs/7cxd08qq#watchexperiment)

If the user opts to monitor the experiment for updates, the system periodically checks for updates and displays them in real-time. This ensures that the user is always informed about the latest status and changes in the experiment without having to manually refresh the information.

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
