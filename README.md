# Create-a-VPC-Peering-Connection

<h2>Description</h2>

This school project revolves around creating a Highly Available AWS environment using Workbench - Vocareum. 

<h2>Task 1: Creating a VPC Peering Connection</h2>

1. In the AWS Management Console, on the Services menu, choose VPC.
2. In the left navigation pane, choose Peering Connections.
3. Choose Create Peering Connection and configure:
    - Peering connection name tag: Lab-Peer
    - VPC (Requester): Lab VPC
    - VPC (Accepter): Shared VPC
    - Choose Create Peering Connection then choose OK
When a VPC peering connection is created, the target VPC must accept the connection request. The target VPC must accept the request because it might be owned by a different account. Alternatively, the user that creates the peering connection might not have permission to accept the connection request for the target VPC. However, in this lab, you will accept the connection yourself.

8. Select Lab-Peer.
9. Choose Actions then select Accept Request, and choose Yes, Accept to accept the request.
10. In the pop-up box, choose Close.

<p align="center">
<br/>
<img src="https://i.imgur.com/gUbAhGp.png"/>

<h2>Task 2: Configuring Route Tables </h2>

1. In the left navigation pane, choose Route Tables.
2. Select  Lab Public Route Table (for Lab VPC). You will configure the Public Route Table associated with Lab VPC. If the destination IP address falls in the range of Shared VPC, the Public Route Table will send traffic to the peering connection.
3. In the Routes tab, choose Edit routes then configure these settings:
    - Choose Add route
    - Destination: 10.5.0.0/16 (The setting is the Classless Inter-Domain Route, or CIDR, block range of Shared VPC.)
    - Target: Select Peering Connection, and then from the list, select Lab-Peer.
    - Choose Save routes then choose Close.
    - You will now configure the reverse flow for traffic that comes from Shared VPC and goes to Lab VPC.

4. Select  Shared-VPC Route Table. If the check boxes for any other route tables are selected, clear them. This route table is for Shared VPC. You will now configure it to send traffic to the peering connection if the destination IP address falls in the range of Lab VPC.
5. In the Routes tab, choose Edit routes then configure these settings:
    - Choose Add route
    - Destination: 10.0.0.0/16 (This setting is the CIDR block range of Lab VPC.)
    - Target: Select Peering Connection, and then from the list, select Lab-Peer.
    - Choose Save routes then choose Close. The route tables are now configured to send traffic via the peering connection when the traffic is destined for the other VPC.

<p align="center">
<br/>
<img src="https://i.imgur.com/6jaLYeW.png"/>

<h2>Task 3: Testing the VPC peering connection </h2>

Now that you configured VPC peering, you will test the VPC peering connection. You will perform the test by configuring the Inventory application to access the database across the peering connection.
1. On the Services menu, choose EC2.
2. In the left navigation pane, choose Instances.
3. Copy the IPv4 Public IP address that is shown in the Description tab.
4. Open a new web browser tab with that IP address. You should see the Inventory application and the following message: "Please configure settings to connect to database"
5. Choose Settings and configure:
    - Endpoint: Paste the database endpoint. To find this endpoint, select Details. Next to AWS, choose Show. Then, copy the Endpoint.
    - Database: inventory
    - Username: admin
    - Password: lab-password
    - Choose Save. The application should now show data from the database. This step confirms that the VPC peering connection was established because Shared VPC does not have an internet gateway. The only way to access the database is through the VPC peering connection.

<p align="center">
<br/>
<img src="https://i.imgur.com/xphkSFQ.png"/>


