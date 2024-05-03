# Elastic-Stack-SIEM

<h2>Description</h2>

In this lab, I'll be setting up an Elastic SIEM using the web portal for Elastic Stack and a Kali Linux VM. SIEM stands for Security Information and Event Management and it's a solution that collects, analyzes and correlates log data from a wide range of sources that is used to detect and respond to security threats in real-time. Elastic Stack is a collection of open-source SIEM tools that provides storage, search, and analysis functions.

These tools are:
<ul>
  <li>Elasticsearch (query/analytics) </li>
  <li>Logstash (log colleciton/normalization) </li>
  <li>Kibana (visualization) </li>
  <li>Beats (endpoint collection agents) </li>
</ul>

<h2>Prerequisites</h2>

<ul>
  <li>VBox or VMware </li>
  <li>Kali Linux VM </li>
  <li>Elastic Stack account </li>
</ul>

<h2>Creating an Elastic Stack Account</h2>

<ol>
  <li>Head over to <a href="https://cloud.elastic.co/login">Elastic Stack</a> to sign up for a free trial.  </li>
  <li>In the home page, click on "Create a deployment." </li>
  <li>Name your deployment and keep the default settings. </li>
  <li>Click on "Create Deployment." and wait for the configuration to be done. </li>
  <li>When deployment is done click on "Continue." </li>
</ol>

<h2>Setting up the VM</h2>

<ol>
  <li>Download Kali Linux from the <a href="https://www.kali.org/get-kali/#kali-virtual-machines">website.</a></li>
  <li>Create a new VM using the file downloaded from the site in either VBox or Vmware. </li>
  <li>Start the VM and follow the prompts on the screen to install Kali, choose your credentials for the username and password. </li>
</ol>

<h2>Configure Agent for Log Collection</h2>
If you aren't familiar with what an agent is, it's a component installed on an endpoint (device) to collect and transmit data (logs, events, and metrics) to the SIEM system for analysis. <br>
This is important to know because we need to set up the agent to collect data from the VM and send it to the Elastic SIEM.

<ol>
  <li>
    Open the sidebar menu located on the top left and click on "Add integrations." bottom. </br>
    <img src="https://github.com/horeacio/SIEM-Lab-with-Elastic/assets/100793672/a9ecc03a-c666-42cf-a76b-60cb4d865b13">
</li>
  <li>
    Look for Elastic Defend and click on "Add Elastic Defend." </br>
    <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/535ccc8a-9580-438d-824b-af5cb4275e02'>
  </li>
  <li>Click on "Install Elastic Defend" and follow the instructions to install the agent to your VM.</li>
  <li>Copy the install code and paste it in your Kali VM. </br>
    <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/88378521-75e5-42b9-b810-058ea118e68f'>
  </li>
  <li>When the agent is done downloading, you can verify the status of it using: <code>sudo systemctl status elastic-agent.service</code>. </br>
    <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/f537b986-da6d-4859-a418-3e2a8401d66c'>
  </li>
</ol>

<h2>Generating Security Events</h2>

To verify the agent is running properly we can start generating some security events on our VM. We can do this by using Nmap. Nmap is an open-source tool used during the reconnaissance stage of a cybersecurity attack. It scans a target host for open ports that can then be used during the exploit stage. </br>

If this is your introduction to Nmap, I suggest you take this time to play with it and get familiar with it. Perform various scans on your VM, not only will this create more logs for your SIEM but it's an important tool to have under your belt and will be beneficial to your cybersecurity career. Use <code>nmap -h</code> to see the different flags incoporated with it. You can start off by using <code>sudo nmap &lt;your ip address&gt;</code> </br>

<center>
  <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/a2b9a8b2-c381-488e-a7a4-8e6a1464ebb0'>
</center>

<h2>Querying Security Events Using Elastic SIEM</h2>

We can now start analyzing the data we generated from the VM to the SIEM.</br>

<ol>
  <li>In the side bar menu, click on "Logs" under the "Observability" blade. 
    <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/3348f0ba-601a-41b9-94ed-76cc5096b965'>
  </li>
  <li>In the search bar, enter <code>process.args: "namp".</code>
    <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/9e7c215e-1d1e-470c-a9f3-cdd64c142746'>
  </li>
  <li>Click on the three dots to view the details of the log. This shows us that this log was generated from the command <code>sudo nmap 10.0.2.15</code> we ran earlier.
    <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/a25a0c57-eb4b-48b1-928a-8fa651b195a8'>
  </li>
</ol>

This is the log from the other scan and it shows us exactly what was executed. <br>
<center>
    <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/5ebc6774-8310-49e6-b7e6-2746a9257033'>
</center>

We can query other events and see the different security events collected by the SIEM. This varies from things like attempted logins and even downloads attempted by the agent.

<h2>Visualizing Events</h2>

Visualizing the events can help analyze logs and identify anomalies in the data.

<ol>
  <li>Open the side bar menu and under the "Analytics" blade click on "Dashboards." 
    <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/6abc5c90-31ef-418f-b473-359cab9154a4'>
  </li>
  <li>Click on "Create dashboard." </li>
  <li>Click on "Create visualization."</li>
  <li>In the drop menu next to the brush, click on "Area." 
    <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/b4168277-ece8-4d3b-b579-71c3d653e3df'>
  </li>
  <li>In the "Metrics" section on the right, choose "Timestamp" for horizontal field and "Count" for vertical field. 
    <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/897702e5-136a-4987-aa90-0b873139895f'>
  </li>
  <li>Click on "Save and return" and click on "Save."</li>
</ol>

We now have a visualization that shows the count of events overtime. </br>

<center>
  <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/5138751f-e4c9-4667-bf5b-608f9f605631'>
</center>

<h2>Creating an Alert</h2>

Alerts are used to detect and respond to security events in timely manner. They are created based on predefined rules and can be configured to trigger defined actions. Thinks like if a user tries to download known malware or access a blocked website. For our case, we are going to set an alert for an Nmap scan. 

<ol>
  <li>Open the side bar menu and under the "Security" blade click on "Alerts."
    <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/ae1ca7be-940a-4567-bac9-83591fb6bc9b'>
  </li>
  <li>Click on "Manage rules."</li>
  <li>Click on "Create new rule."</li>
  <li>Select on "Custom query" under "Define rule."
    <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/3e1834f8-d239-4069-a01a-b35846b05d1f'>  
  </li>
  <li>Fill out the details and click on "Continue."
    <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/2fdbd7b0-16c1-412d-8272-2ce6bb1d485d'>
  </li>
  <li>Under "About rule" fill out the name and description for the alert. Set the severity level and click on "Continue."
    <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/52351bdc-c8e0-425b-be7b-4e20411dc289'>
  </li>
  <li>Keep the default options under "Schedule rule" and click on "Continue."</li>
  <li>Under "Rule Actions" set how you want to receive the alerts and the response to the alert. 
    <img src='https://github.com/horeacio/Elastic-Stack-SIEM/assets/100793672/6c220aa1-1521-4bea-8d0d-9fd3f0f34a09'>
  </li>
  <li>Click on "Create & enable rule."</li>
</ol>

Now that the alert has been created, it will monitor incoming logs for an Nmap scan. When triggered, you'll receive an alert in the method chosen and take whatever action was selected. Alerts can be viewed and managed in "Alerts" under the "Security" blade in the side bar menu. 

<h2>Conclusion</h2>

We have now established a SIEM using Elastic Stack, installed an agent on our Kali Linux VM to forward data from the VM to the SIEM, generated logs using Nmap, queried and analyzed logs for Nmap scans, created a visual dashboard to count security events, and created an alert to detect Nmap
