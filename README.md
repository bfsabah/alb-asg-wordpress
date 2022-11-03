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

11- We create our Aplication Load Balancer Security Group (ALBASG) with inbound rules 0.0.0.0/0 --> 80 and 0.0.0.0/0 --> 443

![image](https://user-images.githubusercontent.com/113843658/199602784-26beb271-b787-4921-8f04-e2a778fbaebc.png)

12- We create our BastionHostSG ( with Inbound Rule 0.0.0.0/0 --> 22.
![image](https://user-images.githubusercontent.com/113843658/199603190-718ade2c-5558-46f8-b50b-0d03cc2278fd.png)

13- We create our AppServerSG (App Server Security Group) with 2 Ingress Rules (80,22)

![image](https://user-images.githubusercontent.com/113843658/199652469-47172bdf-f0f3-4aba-b17f-5cd9d5e75e04.png)

14- We create our DMZPublicNACL with Public Subnet Associations.
![image](https://user-images.githubusercontent.com/113843658/199659649-04549fd7-ff28-4513-b308-8092603e9d66.png)

15- We create our Ingress Rules 100, 110, 120, 130

![image](https://user-images.githubusercontent.com/113843658/199667313-5a106021-8c94-446f-9413-bb11e8e07c2f.png)

16 - We create AppLayerPrivateSubnetNACLEgress 100,110,120,130 Rules.
![image](https://user-images.githubusercontent.com/113843658/199774075-8975d2e1-2954-49d5-ab36-cf5719eab789.png)

17- We created AppLayerPrivateNACL and we associate AppLayerPrivate1 and AppLAyerPrivate2 subnets.
![image](https://user-images.githubusercontent.com/113843658/199777506-1bda74a7-fa17-458d-af70-e5d9ecd25e2b.png)

18- We created AppLayerPrivateNACL Ingress 100,110,120 and 130 Rules.
![image](https://user-images.githubusercontent.com/113843658/199781461-15af84ed-3f3f-4219-93b6-351dd08888e1.png)

19 - We create AppLayerPrivateSubnetNACL Egress 100,110,120 and 130 rules.
![image](https://user-images.githubusercontent.com/113843658/199804376-ad66193c-8484-42e4-8013-215f559b243b.png)

20- We create ALB (Apllication Load Balancer) selecting Subnets (Public1 and Public2).
![image](https://user-images.githubusercontent.com/113843658/199812100-91c436f0-61ee-47a7-a216-d8a771c0d57d.png)

21 - We create our Listener.
![image](https://user-images.githubusercontent.com/113843658/199812491-d82733c2-2a37-47cf-8326-e355f109fbb2.png)

22- We create TargetGroup for Load Balancer.
![image](https://user-images.githubusercontent.com/113843658/199812810-45e53b26-c579-40d2-a649-f0bba4124852.png)




