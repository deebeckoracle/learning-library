# Steps to Connect to the Database

## Introduction
In this lab, we will create the connection to primary and standby databases.

Estimated Lab Time: 15 Minutes

### Objectives
- Create a database connection to the primary database
- Create a database connection to the standby database

## Task 1: Create the Connection to the primary

<if type="livelabs">

1. Open up the menu in the left hand corner.  

2. From the menu, select **Oracle Database**, then **Bare Metal, VM, and Exadata**.

  ![](https://raw.githubusercontent.com/oracle/learning-library/master/common/images/console/database-dbcs.png " ")

3. In the List Scope section on the left, enter the first part of the compartment assigned to you in the Search field, then click the compartment name.

  ![](images/select-compartment-livelabs.png)


   There are two Database Systems created for you. The system prefixed with `ADGHOLD1` is your primary database, and the system prefixed with `ADGHOLD2` is your secondary database.

</if>

1. Click the name of the primary database (`ADGHOLD1`).

  ![](images/db-systems-livelabs.png)

  Scroll down on the page and click on **Nodes(1)** to find on which host it resides.
  The Public IP Address part is the IP Address we want to know. Make a copy of this on the clipboard or make sure to have this information noted down.

  ![](./images/nodes-1.png)

5. Open the **Cloud Shell** using the icon next to the region.

  ![](./images/cloud-shell.png)

  The Cloud Shell opens after a few seconds and shows the **prompt**.

7. Find your ssh private key which has been created earlier to connect to the host where the primary database is located.

  Using the **Upload** facility, upload the private key in the **Cloud Shell** environment.

  ![](./images/cloud-shell-upload.png)

  ![](./images/cloud-shell-upload-key.png)

8. Change the permission of the private key to `0600` and connect to the primary host as `opc`, using the public IP address that you have noted down earlier.
    ````
    <copy>chmod 600 cloudshellkey</copy>
    ````
    Replace `cloudshellkey` with the name of your private key file.
    ````
    <copy>ssh -i cloudshellkey opc@IP_ADDRESS</copy>
    ````
    Replace `cloudshellkey` with the name of your private key file, and `IP_ADDRESS` with the real public IP address.



9. You should be connected to the primary database host. You can become **oracle** with `sudo su - oracle` and connect to the instance with the command `sqlplus / as sysdba` and execute a query:

    ````
    <copy>Select name, db_unique_name, database_role from v$database;</copy>
    ````

  ![](./images/connect-primary.png)


## Task 2: Create the Connection to the Standby in a new tab

1. **Duplicate the tab in your browser**. If your browser does not support tab duplication, open a new tab and connect again to the **Cloud Console**.

2. From the menu, navigate again to **Oracle Database**, then  **Bare Metal, VM and Exadata**.

  This time, select the **ADGHOLAD2** DB System (the standby database).

  ![](images/db-systems-livelabs.png)

  Scroll down on the page and click on **Nodes(1)** to find on which host it resides.
  The Public IP Address part is the IP Address we want to know. Make a copy of this on the clipboard or make sure to have this information noted down.

  ![](./images/nodes-2.png)

5. Open the **Cloud Shell** using the icon next to the region.

  ![](./images/cloud-shell.png)

  The Cloud Shell opens after a few seconds and shows the **prompt**.

7. The private key that you have uploaded in the previous step should already be there. The same key can be used to connect to the standby database host.

  Connect to the standby host as `opc`, using the public IP address that you have noted down earlier.
    ````
    <copy>ssh -i cloudshellkey opc@IP_ADDRESS2</copy>
    ````
    Replace `cloudshellkey` with the name of your private key file, and `IP_ADDRESS2` with the public IP address of the standby database host.

9. You should be connected to the standby database host. You can become **oracle** using `sudo su - oracle` and connect to the instance with the command `sqlplus / as sysdba` and execute a query:

    ````
    <copy>Select name, db_unique_name, database_role from v$database;</copy>
    ````

  ![](./images/connect-standby.png)

You have now successfully created a database connection to the primary and the standby database.

## Acknowledgements

- **Author** - Pieter Van Puymbroeck, Product Manager Data Guard, Active Data Guard and Flashback Technologies
- **Contributors** - Robert Pastijn, Ludovico Caldara, Suraj Ramesh
- **Last Updated By/Date** -  Ludovico Caldara, October 2021
