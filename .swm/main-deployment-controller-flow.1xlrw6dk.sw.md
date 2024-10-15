---
title: Main Deployment Controller Flow
---
This document will cover the Main Deployment Controller Flow, which includes:

1. Setting Up the Command
2. Initializing the Manager
3. Running the Controller
4. Running the Worker

Technical document: <SwmLink doc-title="Main Deployment Controller Flow">[Main Deployment Controller Flow](/.swm/main-deployment-controller-flow.symz5qdt.sw.md)</SwmLink>

# [Setting Up the Command](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=/docs/symz5qdt#setting-up-the-command)

The process begins with setting up the command, which involves configuring various options and parameters necessary for the deployment controller. This includes initializing client configurations, logging settings, and other essential parameters. Additionally, it sets up signal handling for graceful shutdowns and initializes various Kubernetes clients and informers. This step ensures that the deployment controller has all the necessary configurations to operate correctly.

# [Initializing the Manager](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=/docs/symz5qdt#initializing-the-manager)

Once the command is set up, the next step is to initialize the manager. The manager is responsible for overseeing the various controllers. Depending on the enabled controllers, it either initializes an Analysis Manager or a general Manager. The Analysis Manager handles analysis runs, while the general Manager manages rollouts, services, ingress, experiments, and analysis runs. This step ensures that the appropriate manager is in place to handle the specific tasks required by the deployment controller.

# [Running the Controller](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=/docs/symz5qdt#running-the-controller)

After the manager is initialized, the controller threads are started. This involves initializing worker threads that process items from the work queue. The controller ensures that all workers are started and waits for the context to be done before stopping the workers. This step is crucial for maintaining continuous processing of deployment tasks, ensuring that the system remains responsive and efficient.

# [Running the Worker](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=/docs/symz5qdt#running-the-worker)

The final step in the flow is running the worker. The worker is a long-running function that continually reads and processes messages from the work queue. This ensures that the work queue is processed continuously, allowing the deployment controller to handle tasks efficiently and effectively. This step is essential for maintaining the smooth operation of the deployment controller, ensuring that all tasks are processed in a timely manner.

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
