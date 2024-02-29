# How-to-lauch-EC2-with-CloudFormation-userdata-
How to lauch EC2 with CloudFormation(+userdata) 

#Crete your Stack with Cloud formation
# Create a yml file and put this code : 
Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: us-east-1a
      ImageId: ami-a4c7edb2
      InstanceType: t2.micro
      KeyName: replication  # Remplacez par le nom de votre paire de clés
      SecurityGroupIds:
        - sg-09912f45eeb865a0c  # Remplacez par l'ID de votre groupe de sécurité existant
      UserData:
        Fn::Base64: |
          #!/bin/bash
          yum update -y
          yum install httpd -y
          echo "<html><body><h1>Bonjour restart</h1></body></html>" > /var/www/html/index.html
          service httpd start
          chkconfig httpd on
          service httpd restart

Outputs:
  InstanceId:
    Description: ID de l'instance EC2 nouvellement créée
    Value: !Ref MyInstance

#Upload the file 


It's done !!
