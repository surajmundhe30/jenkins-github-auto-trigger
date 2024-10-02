
# Jenkins Pipeline Auto Trigger on GitHub Push

This guide walks you through setting up an automated Jenkins pipeline that triggers when changes are pushed to the `master` branch of a GitHub repository.

## Prerequisites

- Jenkins server up and running.
- GitHub repository.
- Jenkins plugins installed:
  - **GitHub Integration Plugin**
  - **Pipeline Plugin**
  - **Git Plugin**
- Jenkins should be publicly accessible to receive GitHub webhook requests.

---

## Step 1: Set Up Jenkins Pipeline Job

### 1.1 Create a New Pipeline Job
1. Go to your **Jenkins Dashboard**.
2. Click on **New Item**.
3. Enter a name for your job (e.g., `Master-Branch-Pipeline`).
4. Select **Pipeline** as the project type.
5. Click **OK**.

### 1.2 Configure the Job
1. In the **Pipeline** configuration:
   - Set **Definition** to **Pipeline script from SCM**.
   - Under **SCM**, choose **Git**.
   - In the **Repository URL**, enter your repository's URL:
     ```
     https://github.com/<your-username>/<your-repo-name>.git
     ```
   - Add your **Credentials** (if the repository is private).
   - In **Branches to build**, specify:
     ```
     */master
     ```
   - Ensure the **Script Path** is correct. If your `Jenkinsfile` is in the root directory, set it to:
     ```
     Jenkinsfile
     ```

### 1.3 Set Up Build Triggers
1. Scroll down to the **Build Triggers** section.
2. Check **GitHub hook trigger for GITScm polling**.

### 1.4 Save the Job Configuration
1. Click **Save** to finalize the configuration.

---

## Step 2: Configure GitHub Webhook

### 2.1 Add a Webhook in GitHub
1. Go to your **GitHub repository**.
2. Click on **Settings**.
3. Select **Webhooks** from the sidebar.
4. Click **Add webhook**.

### 2.2 Set the Webhook Details
1. In the **Payload URL** field, enter the Jenkins webhook URL:
   ```
   http://<your-jenkins-server-ip>:8080/github-webhook/
   ```
2. Set the **Content type** to `application/json`.
3. In the **Which events would you like to trigger this webhook?** section, choose **Just the push event**.
4. Click **Add Webhook**.

---

## Step 3: Create or Update Jenkinsfile

 In your repository, create a `Jenkinsfile` in the root directory (if it doesn’t already exist).

## Step 4: Test the Setup

1. Push changes to the `master` branch of your GitHub repository.
2. Jenkins should automatically trigger the pipeline when the push event is received.
3. Check the **GitHub webhook** delivery status:
   - Go to **GitHub > Settings > Webhooks**.
   - Check the **Recent Deliveries** to ensure the webhook is being delivered with a `200 OK` response.
   
4. Verify that the build is triggered on Jenkins.

---

## Troubleshooting

- **Webhook not triggering the build?**
  - Check if Jenkins is publicly accessible.
  - Ensure the webhook URL is correct (`http://<your-jenkins-server-ip>:<port>/github-webhook/`).
  - Check **Jenkins Logs** (`Manage Jenkins > System Log`) for any errors.
  
- **Pipeline not executing for the correct branch?**
  - Ensure the **branch filter** in the `Jenkinsfile` is correctly set to `master`:
    ```groovy
    when {
      branch 'master'
    }
    ```

---

## Conclusion

By following these steps, you have set up a Jenkins pipeline that automatically triggers when someone pushes code to the `master` branch of your GitHub repository.

Feel free to customize the pipeline stages and steps as per your project's requirements.
