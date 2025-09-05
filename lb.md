Q. Use of load balancer - create 4 instances in different zones - same security group (imp)

Go to load balancing

Create Target group

choose instances name it next and add the machines - include as pending below create target group

Now go to - Load Balancer Create application load balancer

Name it Internet facing (for databse it should be internal) IPv4

select the zones in which you had made the instances (a,b,c,d)

select the same security group as instance

select http and target group then create load balancer

Now go to load balancer

wait for it to get active Now select the load balancer created Scroll and copy the DNS name and paste it on website

Now to check - go on any machine terminal and systemctl stop httpd

Now refresh the webpage and you will see bad gateway - later in the target group amazon will put the machine to unhealthy and stop diverting requests to it

TO ENABLE SESSION STICKINESS

Go to target groups - select your target group Go to actions - edit target group attributes

Target selection configuration - stickiness - turn on - duration 1 - days save changes

Now refresh the webpage the server wont change -
