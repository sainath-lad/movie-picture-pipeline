## GitHub Repository

https://github.com/sainath-lad/movie-picture-pipeline

## GitHub Actions — Successful Workflow Runs

Frontend CI 
https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/39151014087

Frontend CD
https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/39032991957 (Earlier successful run)

https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/39210283058 (Latest run with below explained issue)

Backend CI
https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/39210602731

Backend CD
https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/39029504091 (Earlier successful run)

https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/39210738305 (Latest run with below explained issue)


## Deployment Issue and Supporting Evidence

I have implemented the frontend and backend CI/CD workflows and addressed the feedback from my previous review.

The frontend and backend CI workflows are passing, including their linting, testing, and Docker build stages.

However, I encountered an AWS EKS infrastructure issue that is preventing the applications from being deployed successfully. The cluster is active, but kubectl get nodes returns No resources found. The frontend, backend, and CoreDNS pods remain in the Pending state, with Kubernetes reporting FailedScheduling: no nodes available to schedule pods.

During earlier troubleshooting, the worker-node initialization logs reported an explicit AWS Organizations Service Control Policy denial involving ec2:DescribeInstances. I have contacted udacity support for assistance but have not received a response yet.

I have included my public GitHub repository, the available GitHub Actions workflow runs, and application endpoint information for verification. The application URLs may remain unavailable until the infrastructure issue is resolved.

I request that the reviewer consider this documented infrastructure limitation and advise me on the appropriate next steps.


## Application URLs

Frontend
http://a4cdd5a309519415288ee6ab1a0540a9-53543498.us-east-1.elb.amazonaws.com

Backend API
http://a159050680d0047bfb52651cdf2f097d-1730096371.us-east-1.elb.amazonaws.com/movies


## Available Screenshots

Frontend URL Screenshot
<img width="1774" height="828" alt="frontend url ss" src="https://github.com/user-attachments/assets/36153a19-dfcf-4fc1-b468-96b1176ac1c6" />


Backend URL Screenshot
<img width="1766" height="891" alt="backend url ss" src="https://github.com/user-attachments/assets/80d0efcd-4a76-4c58-9609-621707077819" />
