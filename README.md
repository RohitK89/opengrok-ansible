OpenGrok
=========

An Ansible role that installs and deploys OpenGrok.
For more info on OpenGrok, see: https://opengrok.github.io/OpenGrok/

Installation
------------

Install the role through Ansible Galaxy:

`ansible-galaxy install RohitK89.opengrok-ansible`

You can then deploy OpenGrok by writing a custom playbook to suit your needs, or by using the ones in the examples folder.

`sudo ansible-playbook deploy_without_ldap.yml`

Requirements
------------

N/A

Role Variables
--------------

####Defaults
`opengrok_base_dir`: The root dir in which OpenGrok should create all the further listed subfolders

`opengrok_src_root`: Where all your code that is to be indexed will be stored

`opengrok_user_basedir`: The home dir for the OpenGrok user that will be created

`opengrok_root`: The root dir where the OpenGrok binary will be set up

`opengrok_data_dir`: The dir where OpenGrok will store its data - index files, configs, etc.

`opengrok_version`: What version of OpenGrok to pull down and set up

`opengrok_pkg_url`: The full URL from where to download whatever version of OpenGrok you wish to set up

`opengrok_env`:

* `OPENGROK_TOMCAT_BASE`: Tomcat's base dir, under which the webapps and config folders are located.
* `OPENGROK_INSTANCE_BASE`: Path to the OpenGrok binary containing folder
* `OPENGROK_VERBOSE`: For logging purposes

`opengrok_java_home`: Path where the default jvm lives. Since java likes to add the machine type and extra info at the end, the default is a wildcard path that works across all types of unix machines.

`opengrok_tomcat_conf_dir`: Path where tomcat's server config files live

`opengrok_add_security`: If set to true, will add LDAP authentication to tomcat. Note: You must provide values for vars listed in the LDAP security section below.

####Vars file
`opengrok_pkg_jdk`: Package name to use for downloading jdk using the default package manager for your system (eg. apt, yum)

`opengrok_pkg_ctags`: Package name to use for downloading ctags

`opengrok_pkg_tomcat`: Package name to use for downloading tomcat

####LDAP Security vars
`opengrok_add_ldaps`: true/false val determining whether you wish to add LDAPS authentication

`opengrok_ldap_cert`:

* `public_key`: The public key to use for talking with your LDAP server
* `filename`: The name of the file in which the key will be saved

`opengrok_tomcat_xml_ldap_addition`: The block of XML to add to Tomcat's server config defining your JNDI realm (for more help, see: https://tomcat.apache.org/tomcat-7.0-doc/realm-howto.html#JNDIRealm

`opengrok_remove_user_db_realm`: true/false value specifying whether or not to remove the User Database realm as a valid authentication mechanism for Tomcat

`opengrok_source_xml_ldap_addition`: The block of XML to add to OpenGrok's webapp's config specifying which LDAP roles are allowed access. The sample provided in the examples folder will allow all users with valid credentials to your LDAP server access to OpenGrok.
