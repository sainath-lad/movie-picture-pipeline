# Movie Picture Pipeline — Submission Evidence

## 1. GitHub Repository

Public GitHub Repository:

https://github.com/sainath-lad/movie-picture-pipeline

The repository contains the frontend and backend applications, Docker configurations, Kubernetes manifests, Terraform configuration, and the four required GitHub Actions workflows.

## 2. GitHub Actions — Workflow Runs

### Frontend Continuous Integration

Status: SUCCESSFUL

https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/39151014087

The workflow successfully completes the frontend linting, testing, and Docker build stages.

### Backend Continuous Integration

Status: SUCCESSFUL

https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/39210602731

The workflow successfully completes backend linting, testing, and Docker image building.

### Frontend Continuous Deployment

Earlier successful run:

https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/39032991957

Latest run:

https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/39210283058

The latest run successfully completed the frontend linting, testing, Docker image build and push, AWS authentication, and EKS kubeconfig configuration.

However, the Kubernetes deployment stage failed with:

`deployment "frontend" exceeded its progress deadline`

The deployment could not complete because the EKS cluster had no registered worker nodes available to schedule the application pods.

### Backend Continuous Deployment

Earlier successful run:

https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/39029504091

Latest run:

https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/39210738305

The latest run successfully completed backend linting and testing.

However, the Docker image build stage encountered an Amazon ECR Public error:

`429 Too Many Requests — Data limit exceeded`

The error occurred while retrieving the Python base image:

`public.ecr.aws/docker/library/python:3.10-alpine`

I subsequently prepared an authentication correction for the ECR Public login in my backend deployment workflow. However, I could not verify the correction through another deployment run because my AWS Learner Lab budget was exhausted.

## 3. AWS EKS Infrastructure Issue

During deployment troubleshooting, I encountered an issue with the EKS worker-node initialization.

The EKS cluster was reported as ACTIVE, and the managed node group was also reported as ACTIVE.

However, the Kubernetes cluster did not have any registered worker nodes.

The command:

`kubectl get nodes -o wide`

returned:

`No resources found`

The frontend, backend, and CoreDNS pods remained in the Pending state.

Kubernetes events repeatedly reported:

`FailedScheduling: no nodes available to schedule pods`

As a result, Kubernetes could not schedule the application pods or complete the deployments.

### Worker Node Initialization — AWS Organizations SCP Restriction

During further investigation, the worker initialization logs repeatedly reported:

`403 UnauthorizedOperation`

The specific denied operation was:

`ec2:DescribeInstances`

The logs identified an explicit AWS Organizations Service Control Policy (SCP) denial affecting the EKS worker-node IAM role.

The initialization process subsequently reported:

`exceeded max wait time for InstanceCondition waiter`

and:

`Failed to start nodeadm-reconcile - EKS Nodeadm Config`

The worker node therefore could not complete initialization and register with the Kubernetes cluster.

This is the primary infrastructure issue preventing the frontend and backend applications from being deployed successfully.

## 4. AWS Learner Lab Budget Exhaustion

While investigating and attempting to resolve the infrastructure issue, my AWS Learner Lab budget was exhausted.

The Udacity workspace displayed:

`Your lab budget has run out. Your work is saved, but you'll need additional hours to keep running labs.`

It also displayed:

`Something went wrong starting this lab. Please try again.`

Consequently, I am currently unable to restart the AWS environment, collect fresh infrastructure diagnostics, or verify the remaining deployment changes.

## 5. Udacity Support Contact History

I contacted Udacity Student Support regarding the AWS infrastructure and lab-access issues.

I received the following email notifications:

- Ticket **2213959** — Confirmation of receiving my support request on 18 October 2026.
- Ticket **2214989** — Support update regarding the inability to launch the console on 25 October 2026.

However, when I revisited the Udacity Help Center on 18 November 2026, my support dashboard displayed:

`No requests found`

The previously accessible support request page also displayed a page-not-found message.

I have retained the support email acknowledgements and dashboard screenshots as evidence that I attempted to seek assistance.

As of 18 November 2026, I have not received a technical resolution for the EKS worker-node restriction or the exhausted AWS Learner Lab budget.

## 6. Application Endpoints

The following LoadBalancer endpoints were previously provisioned for the project.

### Frontend Application

http://a4cdd5a309519415288ee6ab1a0540a9-53543498.us-east-1.elb.amazonaws.com

### Backend Movies API

http://a159050680d0047bfb52651cdf2f097d-1730096371.us-east-1.elb.amazonaws.com/movies

Both endpoints were accessible previously, and the available historical screenshots demonstrate the frontend movie list and backend API response.

Their current availability could not be verified after the AWS infrastructure issue occurred.

## 7. Request for Reviewer Consideration

I have implemented all four required GitHub Actions workflows and successfully completed the frontend and backend CI requirements.

I also addressed the previous review feedback and continued troubleshooting the CD pipelines.

However, the remaining deployment verification has been blocked by two issues:

1. An explicit AWS Organizations SCP denial involving `ec2:DescribeInstances`, which prevents the EKS worker node from completing initialization and registering with the cluster.
2. Exhaustion of the AWS Learner Lab budget, which prevents me from continuing the deployment troubleshooting and verifying the latest backend ECR authentication correction.

I have contacted Udacity Support and retained the available acknowledgement emails and technical evidence, but the issues remain unresolved.

I understand that the project requires successful CD deployments and accessible application endpoints. I am committed to completing these requirements.

I respectfully request the reviewer's consideration of the documented infrastructure restrictions and guidance on an approved alternative, AWS lab extension, or additional opportunity to complete and verify the remaining deployment requirements.

Thank you for reviewing my submission and considering the circumstances.

---

# 8. Supporting Screenshots
<img width="1774" height="828" alt="frontend url ss" src="https://github.com/user-attachments/assets/452bdc27-5369-4474-a921-9844bffe8bda" />

<img width="1766" height="891" alt="backend url ss" src="https://github.com/user-attachments/assets/33a731bc-20b9-4392-a6c4-2aa60e6c781a" />

<img width="636" height="140" alt="no resource found" src="https://github.com/user-attachments/assets/0d35f9cb-6855-4bf5-be5f-ed753529c4ae" />

<img width="1272" height="498" alt="scp denial 1" src="https://github.com/user-attachments/assets/157ebe06-5900-4dc6-83d4-5999c2ea5818" />

<img width="1311" height="515" alt="scp denial 2" src="https://github.com/user-attachments/assets/da58fe28-d55e-4227-a4eb-ebfb2ae48769" />

<img width="1267" height="527" alt="scp denial 3" src="https://github.com/user-attachments/assets/ca9791f8-b412-4436-9dfc-425283e4f638" />

<img width="1262" height="557" alt="scp denial 4" src="https://github.com/user-attachments/assets/7b1f45b9-b21f-441b-adef-2ef6bda1521f" />

<img width="1010" height="547" alt="scp denial 5" src="https://github.com/user-attachments/assets/c5a7c3f7-0161-4a7d-9158-e31a55dfe721" />

<img width="1268" height="542" alt="scp denial 6" src="https://github.com/user-attachments/assets/b2ba44a4-c953-47af-a48a-6ce1589aa6c3" />

<img width="937" height="505" alt="kubernetes pending pods" src="https://github.com/user-attachments/assets/9dd10f96-bf2b-4c9b-abb5-0850da4b236a" />

<img width="1881" height="822" alt="Backend CD ECR error" src="https://github.com/user-attachments/assets/432d6bc2-a4e9-4ebe-ab54-340cb31f7083" />

<img width="1578" height="875" alt="aws credits over" src="https://github.com/user-attachments/assets/1cf9322b-d573-4de2-8aa4-170f95a56649" />

<img width="1553" height="700" alt="udacity support ticket 2214989" src="https://github.com/user-attachments/assets/aefda384-e7fd-4041-92a0-33956f95c714" />

<img width="1542" height="707" alt="udacity support ticket 2213959" src="https://github.com/user-attachments/assets/57eee210-8ce8-436a-95ca-5bbecf31b08f" />

<img width="1825" height="1028" alt="udacity support no requests found" src="https://github.com/user-attachments/assets/7f06800f-9c7a-49ed-90bb-2b492ff5da32" />
