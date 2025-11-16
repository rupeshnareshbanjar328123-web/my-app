🚀 Task 2: Create a Simple Jenkins Pipeline for CI/CD
📌 Objective

Set up a basic Jenkins pipeline to automate the process of building and deploying an application.

🛠 Tools Required

Jenkins

Docker

📦 Deliverable

A Jenkins Pipeline file (Jenkinsfile) that builds and deploys your application.

💡 Steps / Hints
1️⃣ Install Jenkins

You can either:

Install Jenkins locally (via Docker or direct installation), or

Use a cloud-based Jenkins instance.

2️⃣ Create a Jenkinsfile

Inside your project repository, create a file named Jenkinsfile with stages such as:

Build

Test

Deploy

3️⃣ Configure Jenkins Job

Create a new Pipeline Job in Jenkins.

Connect it with your GitHub/GitLab repo.

Enable webhook triggers so the pipeline runs on every code push.

4️⃣ Add Pipeline Stages

Stages typically include:

Checkout code

Build the application

Test the application

Deploy the application

5️⃣ Test the Pipeline

Push changes to your repository and verify the pipeline execution in the Jenkins dashboard.

🎯 Expected Outcome

By completing this task, you will understand how to automate deployments using Jenkins in a CI/CD workflow****
