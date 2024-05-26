### Production-quality Kubernetes cluster build by hands using EC2 instances, then deploy the Object Detection Service in it, in addition to a few more observability tools.
---
#### Technologies used:
<p align="left">
  <a href="https://www.python.org/" target="_blank">
    <img src="https://img.shields.io/badge/Python-%2314354C.svg?style=flat-square&logo=python&logoColor=white" alt="Python">
  <a href="https://www.docker.com/" target="_blank">
    <img src="https://img.shields.io/badge/Docker-%232496ED.svg?style=flat-square&logo=docker&logoColor=white" alt="Docker">
  </a>
  <a href="https://github.com/features/actions" target="_blank">
    <img src="https://img.shields.io/badge/GitHub-232671E5.svg?style=flat-square&logo=github-actions&logoColor=white" alt="GitHub">
  </a>
  <a href="https://aws.amazon.com/" target="_blank">
    <img src="https://img.shields.io/badge/AWS-%23FF9900.svg?style=flat-square&logo=amazon-aws&logoColor=white" alt="AWS">
  </a>
  <a href="https://kubernetes.io/" target="_blank">
    <img src="https://img.shields.io/badge/Kubernetes-%231572B6.svg?style=flat-square&logo=Jenkins&logoColor=white" alt="Kubernete">
  </a>
  <a href="https://grafana.com/" target="_blank">
    <img src="https://img.shields.io/badge/Grafana-%232496ED.svg?style=flat-square&logo=Jenkins&logoColor=white" alt="Grafana">
  </a>
  <a href="https://linux.org/" target="_blank">
    <img src="https://img.shields.io/badge/Linux-%23FF9900.svg?style=flat-square&logo=Jenkins&logoColor=white" alt="Linux">
  </a>
   <a href="https://prometheus.io" target="_blank">
    <img src="https://img.shields.io/badge/prometheus-%2314354C.svg?style=flat-square&logo=Jenkins&logoColor=white" alt="Prometheus">
  </a>


</p>

---

![image](https://github.com/AmiranIV/Provisioned-K8s-Object-Detection/assets/109898333/2611878c-8d3e-4840-af2b-c08e060c5827)

I've successfully completed a project where I deployed an Object Detection Service in a Kubernetes cluster. This project involved several key stages:

* Infrastructure Provisioning: I created a Kubernetes cluster using Ubuntu medium instances. This included one control plane and several worker nodes, all within a VPC having at least two public subnets across different Availability Zones.

* Control Plane Node Setup: On the control plane machine, I set up necessary IAM roles and security groups to ensure secure and seamless communication within the cluster. I installed essential tools like jq and awscli, and chose cri-o as the container runtime for the cluster’s nodes. I also ensured the machine's hostname matched the AWS console for proper Kubernetes-AWS integration.

* Kubernetes Components Installation: I installed Kubernetes tools such as kubeadm, kubelet, and kubectl. I also disabled swap memory and ensured both kubelet and the container runtime used systemd as the init system. For initializing the control plane, I used the kubeadm init command with a configuration file, ensuring all control plane components were correctly deployed.

* AWS Cloud Controller Manager Deployment: This was crucial for linking the cluster with AWS API, allowing proper provisioning and management of AWS resources like EC2 instances and ELBs.

* Pod Network Addon Installation: To enable pod-to-pod communication, I installed a Container Network Interface (CNI) network add-on, choosing the Calico Project for its robust features.

* Worker Node Joining: After setting up another Ubuntu EC2 instance with necessary roles and security measures, I replicated the control plane setup steps and joined this new machine to the cluster as a worker node.

* Cluster Addons Installation: I installed the EBS CSI driver for managing EBS volumes. Additionally, I deployed the Kubernetes Dashboard and configured token-based access for security.

* Object Detection Service Deployment: With the cluster up and running, I deployed the Object Detection Service. This involved creating a GitHub repo for source code management, storing Docker images in DockerHub, and crafting YAML manifests for the polybot and yolo5 microservices. Key considerations were liveness and readiness probes, resource management, autoscaling based on CPU utilization, and graceful service termination.

* Telegram Integration: I integrated the service with Telegram using an Nginx ingress controller and set up a subdomain with a self-signed TLS certificate for secure communication.

* Service Monitoring: For robust monitoring, I deployed Grafana integrated with AWS CloudWatch and a database for log management using FluentD. I also set up Prometheus for detailed cluster metrics, including custom dashboards for node health and Nginx ingress controller metrics.

#### This project not only honed my skills in Kubernetes deployment and management but also in integrating various AWS services and monitoring tools for a comprehensive cloud-native solution.

---

Resources links:

* Container Runtime - https://kubernetes.io/docs/setup/production-environment/container-runtimes/

* Kubeadm install - https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

* Cloud provider aws - https://github.com/kubernetes/cloud-provider-aws

* Network Plugins - https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/

* Installing Calico - https://docs.tigera.io/calico/latest/getting-started/kubernetes/self-managed-onprem/onpremises#install-calico

* Kubernetes Dashboard - https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

* Generate self signed certificate - https://core.telegram.org/bots/webhooks#a-self-signed-certificate

---

![WhatsApp Image 2024-03-31 at 15 36 03](https://github.com/AmiranIV/Provisioned-K8s-Object-Detection/assets/109898333/70967fab-3319-44e8-bf06-15ed45df1f44)
