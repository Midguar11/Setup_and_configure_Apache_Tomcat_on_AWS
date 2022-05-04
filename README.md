# Create AWS instance

- Launch
- Quick setup
- Name tag" Tomcat Server "
- Select Amazon Linux AMI 
- Select T2.micro
- Create New RSA / PEM Keypair

# Open SSH on Power Shell

- Copy keypair master to user/myuser
- Open Power Shell
- ssh -i ccccc.pem ec2-user@myinstance_Ip
- sudo su -

# Dowload Tomcat

- visit site: https://tomcat.apache.org/download-80.cgi
- tar.gz link : https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.78/bin/apache-tomcat-8.5.78.tar.gz
 
      wget https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.78/bin/apache-tomcat-8.5.78.tar.gz
      tar -xvzf apache-tomcat-8.5.78.tar.gz
      ll
      mv apapache-tomcat-8.5.78 tomcat
      cd tomcat
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

    cd tomcat/conf
    ll
    nano server.xml

- edit connector port from 8080 to 8090 " because jenkins same 8080 "

# Start Tomcat

    ./startup.sh

- open webrowser " instances public ip:8090

# Setup role and user data is tomcat-users.xml

    cd tomcat/conf
    nano tomcat-users.xml

- Adding admin, users and robot passwo

      nano /root/tomcat/webapps/manager/META-INF/context.xml

- this change only comment line " <!-- <Valve className="org.apache.catalina.valves.RemoteAddrValve"
         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->   "

      nano /root/tomcat/webapps/host-manager/META-INF/context.xml

this change only comment line " <!-- <Valve className="org.apache.catalina.valves.RemoteAddrValve"
         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->   "

     ./shutdown.sh  
     ./startup.sh   