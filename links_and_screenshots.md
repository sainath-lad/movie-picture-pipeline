## GitHub Repository

https://github.com/sainath-lad/movie-picture-pipeline

## GitHub Actions — Successful Workflow Runs

Frontend CI 
https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/39032992013

Frontend CD
https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/39032991957

Backend CI
https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/38150712610

Backend CD
https://github.com/sainath-lad/movie-picture-pipeline/actions/runs/39029504091


## Application URLs

Frontend
http://a4cdd5a309519415288ee6ab1a0540a9-53543498.us-east-1.elb.amazonaws.com

Backend API
http://a159050680d0047bfb52651cdf2f097d-1730096371.us-east-1.elb.amazonaws.com/movies


## Deployment Note

The frontend and backend were previously deployed to Amazon EKS using
GitHub Actions. The application URLs are provided above.

The AWS worker node subsequently encountered an initialization issue
related to an AWS Organizations policy restriction. Live endpoint availability should be verified during evaluation.

## Available Screenshots

Frontend URL Screenshot
<img width="1774" height="828" alt="frontend url ss" src="https://github.com/user-attachments/assets/36153a19-dfcf-4fc1-b468-96b1176ac1c6" />


Backend URL Screenshot
<img width="1766" height="891" alt="backend url ss" src="https://github.com/user-attachments/assets/80d0efcd-4a76-4c58-9609-621707077819" />
