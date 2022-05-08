<h2 style="text-align: center;"><u>POC - Dockers Edition</u></h2>
<h3 ><u>Please note, nginx configuration is not complete yet!</u></h3>
<p>This is a POC test for DevOps position. It contains Jenkins pipeline running Vgarant script to build one ubuntu VM, Ansible playbooks for building and running dockerized nginx and apache servers and a test phase.</p>
<h4><strong>Prerequisites:</strong></h4>
<p>1. Jenkins Server (v2.332.3) with Ansible plugin (v1.1)</p>
<p>2. Ubuntu 20.04 node with "ubuntu" label attached and the following applications:</p>
<ul>
<li>Oracle VirtualBox (v6.1)</li>
<li>Docker (v20.10.15)</li>
<li>Python (v3.8.10)</li>
<li>Ansible (core v2.12.5, ansible v5.7.1) with</li>
<li>Ansilble community.docker plugin (v.2.4.0)</li>
<li>Vagrant (v2.2.19)</li>
</ul>
<p>&nbsp;</p>
<p>Please pull code from git with Jenkins and run the pipeline or copy the contents of Jenkinsfile in a new pipeline script.</p>
<p>&nbsp;</p>
<h4><strong>Testing:</strong></h4>
<p>After the Ansible provisioning stage, Jenkins will send get requests to the nginx server (192.168.80.80:8080), these requests will be directed to web-1 (127.17.0.2) and web-2 (127.17.0.3) servers in a round-robin pattern, and we'll be able to see that the reply will be received from different server each time.</p>
