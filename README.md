# Create AWS instance

- Launch
- Quick setup
- Name tag" Tomcat Server "
- Select Amazon Linux AMI 
- Select T2.micro
- Create New RSA / PEM Keypair

# Open SSH on Power Shell

- Use Ansible keypair
- Open Power Shell
- ssh my Ansible server
- next connect new server "ssh -i ~/.ssh/Ansible midguard@54.172.185.67"         
- new terminal
- Connect Ansible Controller
- cat Ansible.pub

      sudo su -
      sudo adduser midguard
      sudo nano /etc/sudoers

- add last line " midguard ALL=(ALL) NOPASSWD:ALL  "

      sudo su - midguard  
      sudo adduser midguard
      sudo su - midguard
      mkdir .ssh
      chmod 700 .ssh
      cd .ssh
      touch authorized_keys
      nano authorized_keys

- copy here from Asnible.pub content
- save
- exit
- exit
- ssh -i ~/.ssh/Ansible midguard@54.172.185.67


# Dowload Tomcat

 - Connect ssh ec2-user
 - Chang root

        sudo su -

- visit site: https://tomcat.apache.org/download-80.cgi
- tar.gz link : https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.78/bin/apache-tomcat-8.5.78.tar.gz
 
      wget https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.78/bin/apache-tomcat-8.5.78.tar.gz
      tar -xvzf apache-tomcat-8.5.78.tar.gz
      ll
      mkdir tomcat
      mv apache-tomcat-8.5.78 tomcat
      cd tomcat
      cd apache-tomcat-8.5.78/
      cd bin
      chmod +x shutdown.sh
      chmod +x startup.sh
      yum install java -y

# Setup AWS Instances

- Back AWS webconsole
- Select instances
- Select security
- Select security Grp: Launc wizard
- Select Edit inbound rules
- Custom TCP 
- Port: 8090
- Save rules

# Setup start port to 8090 in config

    cd tomcat/apache-tomcat-8.5.78/conf
    ll
    nano server.xml

- edit connector port from 8080 to 8090 " because jenkins same 8080 "

# Start Tomcat

    ./startup.sh

- open webrowser " instances public ip:8090

# Setup role and user data is tomcat-users.xml

    cd tomcat/apache-tomcat-8.5.78/conf
    nano tomcat-users.xml

- Adding admin, users and robot passwo
" 
 <role rolename="manager-gui"/>
 <user username="xxxxxx" password="xxxxx" roles="manager-gui"/>

 <role rolename="manager-script"/>
 <user username="xxxxxx" password="xxxxx" roles="manager-script"/>

<<<<<<< HEAD
 "

      nano /root/tomcat/apache-tomcat-8.5.78/webapps/host-manager/META-INF/context.xml

- this line modify to comment line " <!-- <Valve className="org.apache.catalina.valves.RemoteAddrValve"
=======
- change this line to comment line " <!-- <Valve className="org.apache.catalina.valves.RemoteAddrValve"
>>>>>>> 8e73a67303cc0ca366ab304631777c589ce0cca9
         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->   "

      nano /root/tomcat/apache-tomcat-8.5.78/webapps/manager/META-INF/context.xml

<<<<<<< HEAD
- this line modify to comment line " <!-- <Valve className="org.apache.catalina.valves.RemoteAddrValve"
=======
change this line to comment line " <!-- <Valve className="org.apache.catalina.valves.RemoteAddrValve"
>>>>>>> 8e73a67303cc0ca366ab304631777c589ce0cca9
         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->   "

     ./shutdown.sh  
     ./startup.sh   
