<h1>Ansible Semaphore Deployment Documentation</h1>

<blockquote>
    <p><strong>Disclaimer:</strong></p>
    <p>This service is provided by a third party. We strive to ensure its security, accuracy, and reliability, but we cannot guarantee that it will be completely free from failures, interruptions, errors, or attacks. Therefore, the company hereby declares: it makes no representations, warranties, or commitments regarding the content, accuracy, completeness, reliability, applicability, or timeliness of this service, and assumes no liability for any direct or indirect losses or damages arising from your use of this service; it assumes no liability for the content, accuracy, completeness, reliability, applicability, or timeliness of third-party websites, applications, products, and services accessed by you through this service, and you shall bear the risks and responsibilities arising from the consequences of use; it assumes no liability for any losses or damages arising from your use of this service, including but not limited to direct losses, indirect losses, loss of profits, loss of goodwill, loss of data, or other economic losses, even if the company has been informed in advance of the possibility of such losses or damages; we reserve the right to modify this disclaimer from time to time, so please check this disclaimer regularly before using this service. If you have any questions or doubts about this disclaimer or this service, please contact us.</p>
</blockquote>

<h2>Overview</h2>

<p>Ansible Semaphore is a modern user interface for Ansible. It allows you to easily run Ansible Playbooks, receive notifications about failures, and control access permissions for deployment systems. If your project has grown to the point where deploying from the terminal is no longer suitable for you, then Ansible Semaphore is what you need.</p>

<p>This document introduces how to activate Ansible Semaphore on Compute Nest, as well as the deployment process and usage instructions.</p>

<h2>Billing Description</h2>

<p>The costs for Ansible Semaphore on Compute Nest mainly involve:</p>
<ul>
    <li>Selected vCPU and memory specifications</li>
    <li>System disk type and capacity</li>
    <li>Public network bandwidth</li>
    <li>Selected RDS database instance specifications</li>
</ul>

<h2>Deployment Architecture</h2>

<!-- Image arch.jpg removed -->

<h2>Required Permissions for RAM Accounts</h2>

<p>The Ansible Semaphore service requires access and creation operations for resources such as ECS, RDS, and VPC. If you use a RAM user to create a service instance, you must add the corresponding resource permissions to the RAM user account before creating the instance. For detailed operations on adding RAM permissions, please refer to <a href="https://help.aliyun.com/document_detail/121945.html" target="_blank">Authorize RAM Users</a>. The required permissions are listed in the table below.</p>

<table border="1" cellspacing="0" cellpadding="5">
    <thead>
        <tr>
            <th>Permission Policy Name</th>
            <th>Remarks</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>AliyunECSFullAccess</td>
            <td>Permission to manage Elastic Compute Service (ECS)</td>
        </tr>
        <tr>
            <td>AliyunRDSFullAccess</td>
            <td>Permission to manage ApsaraDB for RDS</td>
        </tr>
        <tr>
            <td>AliyunVPCReadOnlyAccess</td>
            <td>Read-only permission to access Virtual Private Cloud (VPC)</td>
        </tr>
        <tr>
            <td>AliyunROSFullAccess</td>
            <td>Permission to manage Resource Orchestration Service (ROS)</td>
        </tr>
        <tr>
            <td>AliyunComputeNestUserFullAccess</td>
            <td>User-side permission to manage Compute Nest services</td>
        </tr>
        <tr>
            <td>AliyunCloudMonitorFullAccess</td>
            <td>Permission to manage Cloud Monitor</td>
        </tr>
    </tbody>
</table>

<h2>Deployment Process</h2>

<h3>Deployment Steps</h3>

<p>Click the <a href="https://computenest.console.aliyun.com/service/instance/create/cn-hangzhou?type=user&ServiceId=service-7899150b25e5410fa72f" target="_blank">deployment link</a> to enter the service instance deployment interface. Follow the prompts on the interface to fill in the parameters and complete the deployment.</p>

<h3>Deployment Parameter Description</h3>

<p>During the process of creating a service instance, you need to configure the service instance information. The following details the input parameters for the Ansible Semaphore service instance.</p>

<table border="1" cellspacing="0" cellpadding="5">
    <thead>
        <tr>
            <th>Parameter Group</th>
            <th>Parameter Item</th>
            <th>Example</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="1">Service Instance Name</td>
            <td></td>
            <td>semaphore-2v6o</td>
            <td>Name of the instance</td>
        </tr>
        <tr>
            <td rowspan="1">Region</td>
            <td></td>
            <td>China (Hangzhou)</td>
            <td>Select the region for the service instance. It is recommended to select the nearest region to obtain better network latency.</td>
        </tr>
        <tr>
            <td rowspan="1">Ansible Semaphore Configuration</td>
            <td>Administrator Password</td>
            <td>********</td>
            <td>Password for the Ansible Semaphore administrator account (username: admin).</td>
        </tr>
        <tr>
            <td rowspan="4">ECS Instance Configuration</td>
            <td>Instance Type</td>
            <td>ecs.gn6i-c4g1.xlarge</td>
            <td>ECS instance specification. Choose based on actual requirements.</td>
        </tr>
        <tr>
            <td>System Disk Type</td>
            <td>ESSD Cloud Disk</td>
            <td>ECS instance system disk type. Choose based on actual requirements.</td>
        </tr>
        <tr>
            <td>System Disk Space (GB)</td>
            <td>100</td>
            <td>ECS instance system disk size. Set based on actual requirements.</td>
        </tr>
        <tr>
            <td>Public Network Bandwidth (Mbps)</td>
            <td>5</td>
            <td>ECS instance public network bandwidth size. Set based on actual requirements.</td>
        </tr>
        <tr>
            <td rowspan="3">RDS Instance Configuration</td>
            <td>Database Account</td>
            <td>semaphore</td>
            <td>The account name used to connect to the database.</td>
        </tr>
        <tr>
            <td>Database Account Password</td>
            <td>********</td>
            <td>The password for the database account. Must contain at least three of the following types: uppercase letters, lowercase letters, digits, and special symbols. Length: 8-32 characters. Special characters include: `!@#$%^&*()_+-=`.</td>
        </tr>
        <tr>
            <td>Instance Specification</td>
            <td>mysql.n2m.small.2c</td>
            <td>The specification of the RDS database instance used.</td>
        </tr>
        <tr>
            <td rowspan="3">Network Configuration</td>
            <td>Availability Zone</td>
            <td>Zone K</td>
            <td>Different availability zones within the region.</td>
        </tr>
        <tr>
            <td>VPC Instance ID</td>
            <td>vpc-********</td>
            <td></td>
        </tr>
        <tr>
            <td>VSwitch Instance ID</td>
            <td>vsw-********</td>
            <td></td>
        </tr>
    </tbody>
</table>

<!-- Image params.jpg removed -->

<h3>Verification Results</h3>

<ol>
    <li>
        <p><strong>View Service Instance:</strong> After the service instance is successfully created, the deployment takes approximately 6 minutes. Once deployment is complete, the corresponding service instance will be visible on the page.</p>
        <!-- Image r1.jpg removed -->
    </li>
    <li>
        <p><strong>Access Ansible Semaphore via Service Instance.</strong></p>
        <!-- Image r2.jpg removed -->
    </li>
    <li>
        <p>After entering the corresponding service instance, click the link next to <strong>SemaphoreLoginURL</strong>. Enter the username <code>admin</code> and the administrator password set in the deployment parameters.</p>
        <!-- Image r3.jpg removed -->
    </li>
    <li>
        <p>After completing verification, you can access Ansible Semaphore. Enter a project name and click "<strong>CREATE DEMO PROJECT</strong>" to create a demo project.</p>
        <!-- Image r4.jpg removed -->
        <!-- Image r5.jpg removed -->
    </li>
</ol>

<h2>Help Documentation</h2>

<p>Please visit the Ansible Semaphore User Guide to learn how to use it: <a href="https://docs.ansible-semaphore.com/user-guide/projects" target="_blank">Usage Documentation</a>.</p>
