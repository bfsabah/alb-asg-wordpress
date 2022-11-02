1- we insert our template format with version and description. Webserverkey is very important in this step.
![image](https://user-images.githubusercontent.com/113843658/199592347-3f9da593-9bd5-413c-a7bd-c50539817c10.png)


2- We insert our Resources. We start with our VPC properties.
Type: "AWS::EC2::VPC"
Cidr-Block : We give our IP range for VPC.
Tags: We give a name to our VPC.
![image](https://user-images.githubusercontent.com/113843658/199594591-ef28e7a6-9746-4b76-8f72-8f398c252609.png)

3- We create our Public1 subnet with Cidr-Block and AZ properties (We use a function to select 1st AZ from list- parameter 0).
  We use for VpcId : { "Ref" : "VPC"} our Logical VPC id.
  
![image](https://user-images.githubusercontent.com/113843658/199595753-c37772e0-576e-42ad-ae5b-e143f66e1a93.png)

4- We create our Public2, Private1 and Private2 subnet just changing Cidr-Block, AZ and Name values..
![image](https://user-images.githubusercontent.com/113843658/199596733-e29ed8db-40fe-402e-8d88-5d0ca40f1cf0.png)
![image](https://user-images.githubusercontent.com/113843658/199596796-e5723e64-8d77-4e28-b5a6-70d12b54e504.png)
![image](https://user-images.githubusercontent.com/113843658/199596851-c6c21e9c-4ebd-41d4-a4ce-5ccb4a3abd10.png)

5- We create our InternetGateway ( Orchsky-IGW) and Attach it to our VPC with InternetGateway attachment.
![image](https://user-images.githubusercontent.com/113843658/199597693-aefd0b52-7a8b-4de1-97aa-14b91f04182d.png)

6- We create our RouteTable and PublicRTRoute (0.0.0.0/0 --> IGW)
![image](https://user-images.githubusercontent.com/113843658/199599551-9b0a13db-dc7a-4c55-86ca-5144dd76f90c.png)

7- We make our Public Subnet Associations.
![image](https://user-images.githubusercontent.com/113843658/199599976-061b2f92-8b00-46a6-a61c-364621c64ede.png)

8- We create Our NATGateway to provide an internet connection to our private subnets. (We allocate an ElasticIp for our NATGateway.

![image](https://user-images.githubusercontent.com/113843658/199600230-6ba05428-0559-4b02-b81c-b9f391ee429c.png)

9- We create our PrivateRT(RouteTable) and edit NatGateWayRoute.

![image](https://user-images.githubusercontent.com/113843658/199600917-0b32a777-b01c-4588-a8c3-831187c729da.png)

10- We associate our Private Subnets to PrivateRT.

![image](https://user-images.githubusercontent.com/113843658/199601056-f345454c-ef34-4687-b2e1-496bd35c24fd.png)

11- 
