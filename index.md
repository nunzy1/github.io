---
layout: default
---

Text can be **bold**, _italic_, or ~~strikethrough~~.

[Link to another page](./another-page.html).

There should be whitespace between paragraphs.

There should be whitespace between paragraphs. We recommend including a README, or a file with information about your project.

# Introduction

The ownCloud platform is a flexible and durable open source file synchronization and sharing solution.  The solution includes:

 - ownCloud server, which runs on Linux.
 - Client applications for Microsoft Windows, Max OS X, and Linux.
 - Mobile clients for the Android and Apple iOS operating systems.

This appendix includes specific QuickStart procedures for ownCloud server.  For more information on ownCloud, refer to the [complete documentation set](https://doc.owncloud.com).

## Installing an ownCloud Server with Docker


**Important:** Ensure that you have met the server system requirements, which are documented in the core documentation under [Officially Recommended & Supported Options](https://doc.owncloud.com/server/admin_manual/installation/system_requirements.html).  The section documents [server options](https://doc.owncloud.com/server/admin_manual/installation/system_requirements.html#server) (versions), which ownCloud can add to or change with new releases. The section also provides important notes, deprecations, and [server memory](https://doc.owncloud.com/server/admin_manual/installation/system_requirements.html#memory-requirements) and [database](https://doc.owncloud.com/server/admin_manual/installation/system_requirements.html#database-requirements) requirements.

**Note:** Samples in the procedures that follow are representative.

Perform the following steps.


 1. Pull the latest [ownCloud Docker image](https://hub.docker.com/r/owncloud/server/).

    The image works with a data volume in the host filesystem, and with separate MariaDB and Redis containers.  
  
    The configuration exposes port 8080 for HTTP connections, and mounts the data and MySQL data directories on the host for persistent storage.

 2. On a local machine, create a new project directory.  
  
    `mkdir owncloud-docker-server`  

 3. Download docker-compose.yml from the [ownCloud Docker GitHub repository](https://github.com/owncloud-docker/server) and install it in your new project directory.  
   
        wget https://raw.githubusercontent.com/owncloud-docker/server/master/docker-compose.yml  

 4. Create an .env configuration file, including required settings as shown in the following sample.

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
  
## Enabling User Connections to an LDAP Server
You must have admin privileges to perform this procedure.

This procedure provides the steps necessary to allow a user to connect to an LDAP server using the server’s IP address and port.  The examples in the procedure use 192.0.2.1 as the IP, and 8080 as the port number.

**Important:** The procedure includes only include those steps required to allow a user to connect to an LDAP server using the server’s IP and port.

Perform the following steps.

1. Launch the LDAP Configuration Panel, which includes four tabs.
2. Select the Server tab.
3. In the Host field, enter the URI of your LDAP server. Preface the URI with `ldaps://`

       ldaps://192.0.2.1

4. In the port field, enter 8080.

5. In the User DN field, enter the DN of the user who will have access to the LDAP server.  A sample follows.

        uid=owncloudsystemuser, cn=sysusers,dc=my-company,dc=com

6. In the One Base DN per line field, enter the base DN.
7. Complete your LDAP configuration for other LDAP Configuration Panel tabs, as necessary, by following the procedures under [User Authentication with LDAP](https://doc.owncloud.com/server/10.1/admin_manual/configuration/user/user_auth_ldap.html)

    

 
### Header 3

```js
// Javascript code with syntax highlighting.
var fun = function lang(l) {
  dateformat.i18n = require('./lang/' + l)
  return true;
}
```

```ruby
# Ruby code with syntax highlighting
GitHubPages::Dependencies.gems.each do |gem, version|
  s.add_dependency(gem, "= #{version}")
end
```

#### Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://assets-cdn.github.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
