The first way in which to implement Progressive Delivery in Kubernetes that we are going to learn is by using Kubernetes core Service Networking.

 ## What is Kubernetes Service Networking?
If you have created a Kubernetes Deployment before, you know that you can have several replicas of the same Pod created as part of a Deployment. You may want to create several replicas of your workload for two main reasons:

  * High Availability. If you only have one replica of your workload and the Pod crashes or gets rescheduled, there will be some downtime for your service while the Pod gets restarted.
  * Horizontal Scaling. As your service gets more traffic, you may need to create more replicas of your workload to serve the extra traffic.

So, if you have several replicas of the same Pod, when a client wants to talk to your service, which Pod is selected?

![](./img/png)

This load balancing between the multiple replicas of the same workload is done in Kubernetes through a core virtual object called the Kubernetes Service.

To implement Service Networking, Kubernetes uses a component called kube-proxy, deployed to every node of a Kubernetes cluster:

![](./img/png)

 ##Progressive Delivery using Service Networking
 
kube-proxy updates regularly the list of service and related endpoints that are available. But how does kube-proxy know that a Pod should be part of endpoints pool of a service?

Kubernetes uses regular labels and selectors to create that relation.

If we create a Deployment, we can assign labels to all the pods created and managed by that Deployment. In this example, we have assigned app:website and service:discounts to all the Pods that are part of that Deployment.

When we create the corresponding Kubernetes Service, we add the labels that the Service should select as endpoints for that particular service:

![](./img/png)

kube-proxy will select as Endpoints for that particular service any Pod in the cluster that has at least the labels app:website and service:discounts (Pod needs to have both labels). If a particular Pod has those two labels/values, and it has other labels as well, that Pod will be selected as well. Every Pod in the same Endpoints pool will be selected with the same weight.

To implement Progressive Delivery with Service Networking, the only thing that we need to do is to create a second Deployment with the new version of our workload, but using the exact same labels as the ones in the Service selector:

![](./img/.png)

As the Service will select one of the Pods with the app:website and the service:discounts labels, and every Pod has the same weight within the pool, then 25% of the traffic will go to the newer version of our workload. We are effectively already doing progressive delivery!

Once we start gathering data about the new deployment, and we are happy with the results, we can continue with our progressive delivery by reducing the number of replicas of the first deployment, and increasing the number of replicas of the second one, increasing the percentage of traffic that goes to the new deployment.

In our second lab we are going to practice using this strategy.
