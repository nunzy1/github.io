This appendix includes specific QuickStart procedures for ownCloud platform. 

## Introduction

The ownCloud platform is a flexible and durable open source file synchronization and sharing solution.  The solution includes:

 - ownCloud server, which runs on Linux.
 - Client applications for Microsoft Windows, Max OS X, and Linux.
 - Mobile clients for the Android and Apple iOS operating systems.

For more information on ownCloud, refer to the [complete documentation set](https://doc.owncloud.com).

This appendix includes:
 - [Installing an ownCloud Server with Docker](#install)
 - [Enabling User Connections to an LDAP Server](#enabling)
 - [Adding a User Account](#adding)
 - [Connecting to ownCloud Using a Browser](#connecting)
 
**Note:** Samples in the procedures that follow are representative.

### <a name="install"></a>Installing an ownCloud Server with Docker

**Important:** Ensure that you have met the server system requirements, which are documented in the core documentation under [Officially Recommended & Supported Options](https://doc.owncloud.com/server/admin_manual/installation/system_requirements.html).  The section documents [server options](https://doc.owncloud.com/server/admin_manual/installation/system_requirements.html#server) (versions), which ownCloud can add to or change with new releases. The section also provides important notes, deprecations, and [server memory](https://doc.owncloud.com/server/admin_manual/installation/system_requirements.html#memory-requirements) and [database](https://doc.owncloud.com/server/admin_manual/installation/system_requirements.html#database-requirements) requirements.

Perform the following steps.


 1. Pull the latest [ownCloud Docker image](https://hub.docker.com/r/owncloud/server/).

    The image works with a data volume in the host filesystem, and with separate MariaDB and Redis containers.  
  
    The configuration exposes port 8080 for HTTP connections, and mounts the data and MySQL data directories on the host for persistent storage.

 2. On a local machine, create a new project directory.  
  
    `mkdir owncloud-docker-server`  

 3. Download docker-compose.yml from the [ownCloud Docker GitHub repository](https://github.com/owncloud-docker/server) and install it in your new project directory.  
   
        wget https://raw.githubusercontent.com/owncloud-docker/server/master/docker-compose.yml  

 4. Create an **.env** configuration file, including required settings as shown in the following sample.

        `cat << EOF > .env
        OWNCLOUD_VERSION=10.0
        OWNCLOUD_DOMAIN=localhost
        ADMIN_USERNAME=admin
        ADMIN_PASSWORD=admin
        HTTP_PORT=8080
        EOF`    
 
 5. Build and start your container.  
 
    `docker-compose up -d`
	
 6. Check that your containers have started.  
 
      `docker-compose ps`

    The output of the command shows the ownCloud database, ownCloud, and Redis containers running.  It also shows that ownCloud is accessible on host machine port 8080.

 7. Run the following command.  
 
     `docker-compose logs --follow owncloud`  
  
    If the output shows a significant amount of information being logged to the console, wait a few minutes before performing the next step. 
	
 8. Launch your browser and access the ownCloud UI.  The username and password are the ones you stored in the .env file.  

      [http://localhost:8080](http://localhost:8080/)
  
### <a name="enabling"></a>Enabling User Connections to an LDAP Server
You must have admin privileges to perform this procedure.

This procedure provides the steps necessary to allow a user to connect to an LDAP server using the server’s IP address and port.  The examples in the procedure use 192.0.2.1 as the IP, and 8080 as the port number.

**Important:** The procedure includes only include those steps required to allow a user to connect to an LDAP server using the server’s IP and port.

Perform the following steps.

1. Launch the **LDAP Configuration Panel**, which includes four tabs.

2. Select the **Server** tab.

3. In the **Host** field, enter the URI of your LDAP server. Preface the URI with `ldaps://`

       ldaps://192.0.2.1

4. In the **port** field, enter 8080.

5. In the **User DN** field, enter the DN of the user who will have access to the LDAP server.  A sample follows.

        uid=owncloudsystemuser, cn=sysusers,dc=my-company,dc=com

6. In the **One Base DN** per line field, enter the base DN.

7. Complete your LDAP configuration for other LDAP Configuration Panel tabs, as necessary, by following the procedures under [User Authentication with LDAP](https://doc.owncloud.com/server/10.1/admin_manual/configuration/user/user_auth_ldap.html) .

### <a name="adding"></a>Adding a User Account

You must have admin privileges to perform this procedure.

1. Launch the **User Management** page of the ownCloud Web UI.

    The default view displays a list of users.

2. In the **Username** field, enter the name of the new user.  User names can contain letters, numbers, dashes, underscores, periods, and at signs.

3. In the **Password** field, enter the user’s initial password.

4. Optionally, select the **Groups** dropdown and assign a groups membership.

5. Click **Create**.

6. Fill-in the new user’s full name if it is different from the Username.  Alternatively, you can leave this field blank and let the user complete it.

7. If you want ownCloud to send the new user an email with login information:

    a. Check **send email to new user**.
    
    b. Enter the new user’s email address.

8. If you want to assign group admin privileges to your new user, select the **Group Admin for** dropdown.  Group administrators have the rights to create, edit, and delete users in their assigned groups.

9. Select the **Quota** dropdown to choose a quota other than the default.  The quota is the maximum amount of disk space assigned to the new user.
   
### <a name="connecting"></a>Connecting to ownCloud Using a Browser

Perform the following steps to access your ownCloud server.

1. Launch your web browser.  Currently supported browsers include Firefox 14+, Chrome 18+, Safari 5+, and IE11+ (not compatibility mode).

2. Enter the address of your ownCloud server.

3. Enter your username and password.

4. Optionally, select **Stay logged in**. Note that this option may be disabled depending upon the additional applications included in your ownCloud environment.

5. Click the arrow the right of the password to login.
 

