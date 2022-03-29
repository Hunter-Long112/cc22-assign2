# Overview of Network Architecture
![alt text](https://github.com/Hunter-Long112/cc22-assign2/blob/main/cc22_assign2_diagram_1.png?raw=true)

# Link to my website (really just the apache test page): 
test0-WebAp-45GNI0EK6O8J-1854540610.us-east-1.elb.amazonaws.com

# Steps I took to complete this assignment:
1. The first step I took in completing this assignment was to set up the base layers of the above architecture (everything except for the 
database servers), so that I could test my own YAML file, that deploys a mySQL database server to each of the private subnets. To set up
these base layers, I used the network yaml, then the server and storage yaml, that were provided by the professor.

2. Once I thought the base architecture was setup correctly, I poked and prodded a bit to ensure that it is was. First I hit the load balancers
DNS name, to ensure that it brought up the apache test page. This proved that the load balancer could communicate with the ec2 instances (web servers)
in the private subnet. Second, I wanted to ensure that the ec2 instances were actually deployed to the private subnet, and to do this I simply 
compared ARNs in the AWS console. 

<put pic of private subnet ARN in stack test00, ec2 ARNs in test01, and show that same ec is in the private subnet>

Here it is also worth mentioning that I learned if you're going to use the outputs from one stack in anothey YAML, you have to create a new stack 
with the second YAML (the one using the outputs from the first) because if you try to update a stack using its own outputs, you'll get an error 
like "Cannot import ScalableWebSRVProject-VPCID while it is being processed by exporting stack test00"; where ScalableWebSRVProject-VPCID is the
output I was trying to use and test00 is the stack that created it. There is probably a better way to do this where you can actually use the outputs 
of a stack to update it, but I couldn't figure it out.

3. Next I wrote my YAML, and as mentioned in class this was fairly easy because of how many resources are available online. The hardest (or most interesting) part was using the outputs from other stacks.

4. When I finally did have my YAML written, I of course wanted to prove that the ec2 instances were deployed to the private subnets, and that 
they actually did have a mySQL database running on them. To first prove that they were deployed to the correct location, I again compared ARNs 
in the AWS console.

<insert pic of the ARN of the database ec2s and show that they are in the private subnets above>

After this, I followed the guide that the professor gave us in class to create a jump box manually, in the public subnet, and then ssh into the 
ec2 instances in the private subnets (the web servers). From here I could connect to the mySQL database that was hopefully setup on the ec2s that
my YAML deployed.

<insert terminal output of sshing into the jumpbox, then the web server in the private subnet, then connecting to the db>
