# Elastic-Stack-SIEM

<h2>Description</h2>

In this lab, I'll be setting up an Elastic SIEM using the web portal for Elastic Stack and a Kali Linux VM. SIEM stands for Security Information and Event Management and it's a solution that collects, analyzes and correlates log data from a wide range of sources that is used to detect and respond to security threats in real-time. Elastic Stack is a collection of open-source SIEM tools that provides storage, search, and analysis functions.

These tools are:
<ul>
  <li>Elasticsearch (query/analytics)</li>
  <li>Logstash (log colleciton/normalization)</li>
  <li>Kibana (visualization)</li>
  <li>Beats (endpoint collection agents)</li>
</ul>

<h2>Prerequisites</h2>

<ul>
  <li>VBox or VMware</li>
  <li>Kali Linux VM</li>
  <li>Elastic Stack account</li>
</ul>

<h2>Creating an Elastic Stack Account</h2>

<ol>
  <li>Head over to <a href="https://cloud.elastic.co/login">Elastic Stack</a> to sign up for a free trial.</li>
  <li>In the home page, click on "Create a deployment."</li>
  <li>Name your deployment and keep the default settings.</li>
  <li>Click on "Create Deployment." and wait for the configuration to be done.</li>
  <li>When deployment is done click on "Continue."</li>
</ol>

<h2>Setting up the VM</h2>

<ol>
  <li>Download Kali Linux from the <a href="https://www.kali.org/get-kali/#kali-virtual-machines">website</a></li>
  <li>Create a new VM using the file downloaded from the site in either VBox or Vmware</li>
  <li>Start the VM and follow the prompts on the screen to install Kali, choose your credentials for the username and password.</li>
</ol>

<h2>Configure Agent for Log Collection</h2>
If you aren't familiar with what an agent is, it's a component installed on an endpoint (device) to collect and transmit data (logs, events, and metrics) to the SIEM system for analysis. <br>
This is important to know because we need to set up the agent to collect data from the VM and send it to the Elastic SIEM.

<ol>
  <li>Open the sidebar menu located on the top left and click on "Add integrations." bottom. <br>
      <img src="https://github.com/horeacio/SIEM-Lab-with-Elastic/assets/100793672/a9ecc03a-c666-42cf-a76b-60cb4d865b13">
</li>
</ol>
