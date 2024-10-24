<p align="center">
<img src="https://i.imgur.com/4hzgUaF.jpeg" alt="Azure logo"/>
</p>

<h1>Lab - Deploy a Basic Web Application in Azure App Service and Configure Security Settings</h1>
In this project, you will deploy a basic web application to Azure App Service and then configure various security settings to ensure that the application is secure. Azure App Service is a fully managed platform that lets you build, deploy, and scale web apps quickly. After deployment, you’ll configure settings like SSL/TLS, authentication, and firewalls to secure the app.

Objective:
- Goal: Deploy a web application to Azure App Service and configure its security settings, including SSL/TLS, authentication, access restrictions, and logging.
- Skills Covered: Web app deployment, SSL/TLS configuration, Azure App Service authentication, access restrictions, firewall settings, and monitoring.

Step 1: Create a Web Application in Azure App Service
1.1: Create an Azure App Service
1. Log in to the Azure Portal: Visit portal.azure.com and log in with your Azure account credentials.
2. In the search bar at the top, type App Services and select it from the dropdown menu.
3. In the App Services window, click on Create to start the process of creating a new app service.
4. You’ll be prompted to fill out the following information:
 - Subscription: Choose the appropriate subscription.
 - Resource Group: Create a new resource group (e.g., WebAppResourceGroup) or select an existing one.
 - Name: Enter a unique name for your web app (e.g., MyBasicWebApp).
 - Runtime Stack: Select the programming language and runtime you want (e.g., Node.js, Python, .NET, etc.).
 - Region: Choose a region closest to you or your users for optimal performance.
5. Under App Service Plan, create a new app service plan, which defines the pricing tier and scaling options.
 - Choose a pricing tier that fits your use case (e.g., Basic for small apps or Standard for larger deployments).
6. Once the details are filled out, click Review + Create, then click Create to provision your web app.
   
Step 2: Deploy the Web Application to Azure App Service
2.1: Set Up Local Development Environment
1. Prepare the Code for Deployment: If you don’t already have a web app ready for deployment, you can use a basic template.
For example, create a simple Node.js web app using this code:
<img src="https://imgur.com/78ehqQV.png" alt="Azure"/>

2.2: Deploy Using Git
You can deploy your web application directly from GitHub, Azure Repos, or other source control systems.

1. In the App Service you created, go to the Deployment Center under the Deployment section in the left-hand menu.
2. Select GitHub (or another repository) as the source control for continuous deployment.
3. Authorize Azure to access your GitHub account.
4. Select the repository and branch where your app is located.
5. Click Save to set up continuous deployment. Now, whenever you push code changes to your GitHub repository, Azure will automatically deploy the latest version.
Alternatively, you can use Azure CLI to deploy the app directly from your local machine.

Step 3: Configure Security Settings for the Web App
Once the app is deployed, it’s crucial to secure it. We’ll go through configuring SSL/TLS, authentication, access restrictions, and logging.

3.1: Configure SSL/TLS for Secure Access
SSL/TLS ensures that the communication between your users and the web app is encrypted.

1. In the App Service page, navigate to TLS/SSL Settings in the left-hand menu.
2. Under Protocol Settings, ensure that HTTPS Only is set to On. This will force all HTTP traffic to redirect to HTTPS, securing the communication.
3. To enable SSL certificates:
 - If you have a custom domain, navigate to the Custom domains section.
 - Use App Service Managed Certificates to request a free SSL certificate or upload your own custom certificate.
4. Once the certificate is added, bind it to the custom domain in the TLS/SSL Bindings section.
This ensures that your web app uses secure communication over HTTPS.

3.2: Enable Authentication and Authorization
Azure App Service can integrate with various identity providers (e.g., Azure Active Directory, Facebook, Google) to authenticate users.

1. Go to Authentication/Authorization in the left-hand menu.
2. Turn on App Service Authentication by setting App Service Authentication to On.
3. Under Action to take when request is not authenticated, choose Log in with one of the identity providers to ensure that unauthenticated users are redirected to the login page.
4. Add an identity provider:
 - Click Add Identity Provider.
 - Choose Azure Active Directory, Microsoft Account, Google, Facebook, or Twitter as the identity provider.
 - If you select Azure Active Directory, you can easily connect to your directory, allowing users to log in using their Azure AD credentials.
5. Click Save to apply the authentication settings.
Now, users will need to authenticate themselves using the identity provider you configured before accessing the app.

3.3: Implement Access Restrictions (Firewall)
You can control who has access to your web app by setting up IP restrictions.

1. Navigate to Networking in the left-hand menu of your App Service.
2. Under Access Restrictions, click on Configure Access Restrictions.
3. Click Add Rule to create a new access restriction.
4 Define the following:
- Name: Give the rule a descriptive name (e.g., AllowSpecificIPs).
- Action: Set to Allow for permitted IP ranges.
- Priority: Assign a priority to the rule (lower priority numbers are evaluated first).
- IP Address/CIDR: Enter the IP address or range (e.g., 203.0.113.0/24) that you want to allow.
5. You can create another rule to Deny traffic from other IPs that don’t match the allowed IP range.
6. Once configured, click Save to apply the access restrictions.
This will create a firewall for your web app, restricting access to specific IP addresses or IP ranges.

Step 4: Enable Logging and Monitoring for Security
Monitoring your web app is essential to ensure ongoing security and performance.

4.1: Enable Diagnostic Logs
1. In the App Service page, go to App Service Logs under the Monitoring section.
2. Enable Application Logging (Filesystem) and Web Server Logging. This allows you to capture application and server logs, which are useful for diagnosing issues or detecting malicious activity.
 - Set Retention Period to a suitable value (e.g., 7 days).
3. Click Save to apply these settings.

4.2: Set Up Application Insights
Azure Application Insights provides real-time monitoring of your web app’s performance and user behavior.

1. Go to Application Insights under the Monitoring section.
2. Click Turn On Application Insights to enable it for your web app.
3. Once enabled, you can view detailed performance metrics, including:
 - Request and response times.
 - Failed requests or exceptions.
 - Live telemetry data showing current usage.

4.3: Set Up Alerts for Suspicious Activity
1. Go to Azure Monitor from the main Azure dashboard.
2. In Azure Monitor, click on Alerts and then New Alert Rule.
3. Define conditions such as:
 - Failed login attempts.
 - Unusual spike in traffic.
 - Application errors.
4. Set up alert actions, such as sending an email to your security team if any thresholds are breached.
   
Step 5: Test the Web Application
After configuring the security settings, it’s important to test the deployment to ensure everything works as expected.

1. Test the HTTPS Configuration:
- Open your browser and navigate to your web app’s URL (e.g., https://mybasicwebapp.azurewebsites.net).
- Ensure the site is using HTTPS and that the connection is secure by checking the lock icon in the browser’s address bar.
2. Test Authentication:
- Access your app as an unauthenticated user and confirm that it redirects you to the login page for the identity provider.
3. Test Access Restrictions:
- Try accessing the app from an IP address that’s outside the allowed range to verify the firewall is blocking access.
4. Check Logs:
- Go back to App Service Logs or Application Insights and review the logs to ensure that they are capturing relevant information about user access and any issues.
  
Step 6: Clean Up Resources
If this was a test deployment and you no longer need the app, make sure to clean up the resources to avoid unnecessary charges.

1. Go to the App Services section in the Azure Portal.
2. Select the app you created and click Delete.
3. If you created any custom resource groups or services (e.g., storage accounts, SSL certificates), delete those as well.
   
Project Outcomes
By completing this project, you will have:

- Deployed a basic web application to Azure App Service.
- Configured secure communication using SSL/TLS.
- Set up authentication using identity providers like Azure Active Directory or social logins.
- Implemented access restrictions to control who can access your web app.
- Enabled logging and monitoring to track the app's performance and detect any security issues.
  
This project will provide you with hands-on experience deploying and securing web applications in Azure, which is a critical skill for cloud security engineers and IAM specialists.
