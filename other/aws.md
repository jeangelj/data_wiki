##launch instance

  1. Launch instance
  2. Start Instance (wait for green light: running)
  3. Connect to instance 

##In terminal: (not in remote server instance)

To run instance: ssh -i “key.pem” ubuntu@ec2-XXX-XX-XX-XXX.compute-1.amazonaws.com (copy this from the instance after clicking connect)

To add file to instance: scp –i “key.pem” file.csv ubuntu@ec2-XXX-XX-XX-XXX.compute-1.amazonaws.com:~ 

To save file from instance locally: scp -i "key.pem" -r ec2-user@ec2-52-201-215-27.compute-1.amazonaws.com:output_2.csv  ~/Desktop

##in instance

###install anaconda: 

wget http://repo.continuum.io/archive/Anaconda2-4.0.0-Linux-x86_64.sh

source ~/.bashrc

export PATH="/home/ubuntu/anaconda2/bin:$PATH"

bash Anaconda2-4.0.0-Linux-x86_64.sh

###jupyter notebook in AWS:

screen -S notebook #in Amazon Server terminal create new terminal

jupyter notebook #in new terminal in Amazon server terminal

Control + A

Control + D

exit

ssh -i ~/Downloads/key.pem -L8889/localhost/8888 ubuntu@ec2-107-21-39-180.compute-1.amazonaws.com #make sure you have the up-to-date instance

→ in your local browser enter: localhost:8889

###mount volume (non-empty w file system): 

lsblk #view your available disk devices and their mount points

sudo file -s /dev/xvdf #check if there is a filesystem 

sudo mkdir mount_point #create directory

sudo mount /dev/xvdf mount_point #mount



