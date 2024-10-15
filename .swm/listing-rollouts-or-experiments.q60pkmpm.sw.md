---
title: Listing Rollouts or Experiments
---
This document will cover the process of listing rollouts or experiments. We'll cover:

1. Initializing the command
2. Setting up subcommands
3. Displaying rollouts
4. Monitoring rollout updates

Technical document: <SwmLink doc-title="Listing Rollouts or Experiments">[Listing Rollouts or Experiments](/.swm/listing-rollouts-or-experiments.l477e5mn.sw.md)</SwmLink>

# [Initializing the command](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=/docs/l477e5mn#newcmdlist)

The process begins by initializing the command for listing rollouts or experiments. This command sets up the structure and adds subcommands for listing rollouts and experiments. This step is crucial as it lays the foundation for the subsequent steps by defining the command's purpose and usage.

# [Setting up subcommands](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=/docs/l477e5mn#newcmdlistrollouts)

Next, the command specifically for listing rollouts is set up. This involves configuring options such as namespace and watch mode. The namespace option allows users to specify the scope of the rollouts they want to list, while the watch mode enables continuous monitoring of rollouts for any changes.

# [Displaying rollouts](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=/docs/l477e5mn#displaying-rollouts)

The rollouts are then displayed in a user-friendly table format. This table includes details such as namespace and timestamps if specified. The purpose of this step is to present the rollouts in an organized manner, making it easy for users to understand the current state of their deployments.

# [Monitoring rollout updates](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=/docs/l477e5mn#monitoring-rollout-updates)

Finally, the system monitors changes to rollouts and prints updates. This involves setting up a watch on the rollouts and using a ticker to periodically flush the output. The function maintains a map of previously printed rollout lines to ensure only meaningful changes are displayed. This step ensures that users are kept informed of any significant updates to their rollouts in real-time.

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
