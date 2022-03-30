# Overview Of Network Architecture
![alt text](https://github.com/Hunter-Long112/cc22-assign2/blob/main/cc22_assign2_diagram_1.png?raw=true)

# Link To My Website (really just the apache test page): 
test0-WebAp-45GNI0EK6O8J-1854540610.us-east-1.elb.amazonaws.com

# Steps I Took To Complete Assignments:
1. The first step I took in completing this assignment was to set up the base layers of the above architecture (everything except for the 
database servers), so that I could test my own YAML file, that deploys a mySQL database server to each of the private subnets. To set up
these base layers, I used the network yaml, then the server and storage yaml, that were provided by the professor.

2. Once I thought the base architecture was setup correctly, I poked and prodded a bit to ensure that it is was. First I hit the load balancers
DNS name, to ensure that it brought up the apache test page. This proved that the load balancer could communicate with the ec2 instances (web servers)
in the private subnet. Second, I wanted to ensure that the ec2 instances were actually deployed to the private subnet, and to do this I simply 
compared ARNs in the AWS console. 

Here it is also worth mentioning that I learned if you're going to use the outputs from one stack in anothey YAML, you have to create a new stack 
with the second YAML (the one using the outputs from the first) because if you try to update a stack using its own outputs, you'll get an error 
like "Cannot import ScalableWebSRVProject-VPCID while it is being processed by exporting stack test00"; where ScalableWebSRVProject-VPCID is the
output I was trying to use and test00 is the stack that created it. There is probably a better way to do this where you can actually use the outputs 
of a stack to update it, but I couldn't figure it out.

3. Next I wrote my YAML, and as mentioned in class this was fairly easy because of how many resources are available online. The hardest (or most interesting) part was using the outputs from other stacks.

4. When I finally did have my YAML written, I of course wanted to prove that the ec2 instances were deployed to the private subnets, and that 
they actually did have a mySQL database running on them. To first prove that they were deployed to the correct location, I again compared ARNs 
in the AWS console. After this, I followed the guide that the professor gave us in class to create a jump box manually, in the public subnet, 
and then ssh into the ec2 instances in the private subnets (the web servers).

# Improvements/Things I Need To Figure Out:
+ One imporvement I'd like to make to the git repo is to include screen shots of the 'validaiton' I was doing where I cross check ARNs and such to make
  sure that everything is being deployed to where it should be
+ Also, I don't think I'm deploying the database servers correctly because I could use the jump host that I manually set up in the public subnet to 
  ssh into the ec2 instance in the private subnet that is acting as a web server, but not the ec2 instance that is acting as a database. I tried 
  sshing into the web server then the database from there, and sshing straight into the database host from the jump box but neither worked. 
