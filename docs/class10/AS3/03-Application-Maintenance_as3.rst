Use Case 03: Application Maintenance with AS3
=============================================

OVERVIEW
--------

Application-Maintenance.yaml is a templated Ansible Playbook that demonstrates the ability to change the state (enable/disable/offline) of traffic flowing to web-server(s) in a load balancing pool.

There are times where web servers are taken offline to provide upgrades, troubleshooting, or even replacement. 

This playbook allows the ability to enable, disable or offline a specific or array of pool members (e.g. [hostname]:[port] or [ip address]:[port]); This script can also affect "All" of the members of a selected pool.

RUNNING THE TEMPLATE
--------------------

Running this template assumes that a F5 BIG-IP instance, necessary webservers and Ansible node are available. 

   1. Ensure you are using a terminal from VSCode (UDF --> Ansible-Node --> Access --> Code-Server --> Password: Ansible123! --> Trust --> Terminal --> New Terminal)

   2. Change Directory in the Ansible Host to the use-cases repo previously downloaded

      .. code:: bash
      
         cd ~/f5-bd-ansible-labs/401-F5-AppWorld-Lab/AS3/03-Application-Maintenance-AS3

   3. Run the Ansible Playbook ‘Application-Maintenance.yaml’

      .. code:: bash

         ansible-navigator run Application-Maintenance.yaml --mode stdout

      .. note::

         By default a VIP and pool will be created during the execution of the code, then the code will disable a single node in that created pool.
         
         Modification of the vars/f5_vars.yml file can change the pool, node(s) and state which can be modified within the f5_vars.yml.

TESTING AND VALIDATION
----------------------

This section assumes knowledge of how to operate BIG-IP commands and networking.

**VERIFYING NODE MAINENANCE:**

   **Access Using F5 UDF Console:**

   Using the External Client (UDF --> Components --> External Client --> Access --> Firefox)

      - In the Bookmarks bar you can select the ``Ansible Labs`` Folder and goto ``401 - Labs`` and Select ``Use Case 3`` 
      - OR within the browser you can browse to https://10.1.20.30:8083/ 
      - Browse the page and notice that only NODE2 is the only responsive Node as Node 1 was disabled.


**BIG-IP CONFIGURATION VERIFICATION:**

   **Using F5 UDF:**

   - BIG-IP - (In UDF --> Components --> BIG-IP --> Access --> TMUI)  - This will popup a webpage to access the F5 Login Page

      - Login to the BIG-IP
      - Navigate to Local Traffic --> Pools
      - Change the Partition (Top Right Corner) to "WorkshopExample"
      - Click on the pool you selected while running the playbook
      - View the members of the pool and verify their state based on action choosen while running the playbook

   - Login information for the BIG-IP:
   
      * username: admin 
      * password: **found in the inventory hosts file**