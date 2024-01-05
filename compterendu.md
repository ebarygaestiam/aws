COMPTE RENDU AWS LILO AYMAN ELRIC ILYAN


VPC 1 : 


# Création VPC
aws ec2 create-vpc --cidr-block 10.0.0.0/16 --query Vpc.VpcId --output text

# Tag VPC
aws ec2 create-tags --resources vpc-0738142f5375712ec --tags Key=Name,Value=lilo-vpc1-cli

# Création Subnet Public
aws ec2 create-subnet --vpc-id vpc-0738142f5375712ec --cidr-block 10.0.1.0/24 --availability-zone us-east-1a --query Subnet.SubnetId --output text

# Tag Subnet Public
aws ec2 create-tags --resources subnet-0561dcb3070c008c8 --tags Key=Name,Value=lilo-subnet-public-vpc1

# Création Subnet Private
aws ec2 create-subnet --vpc-id vpc-0738142f5375712ec --cidr-block 10.0.2.0/24 --availability-zone us-east-1a --query Subnet.SubnetId --output text

# Tag Subnet Private
aws ec2 create-tags --resources subnet-08df3732b34bb20fe --tags Key=Name,Value=lilo-subnet-private-vpc1

# Création Internet Gateway
aws ec2 create-internet-gateway --query InternetGateway.InternetGatewayId --output text

# Attacher la Gateway au VPC
aws ec2 attach-internet-gateway --vpc-id vpc-0738142f5375712ec --internet-gateway-id igw-05d3ce61881a91e6a

# Création Table de Routage
aws ec2 create-route-table --vpc-id vpc-0738142f5375712ec --query RouteTable.RouteTableId --output text

# Tag Table de Routage
aws ec2 create-tags --resources rtb-052bf47049505554f --tags Key=Name,Value=lilo-rtb-vpc1

# Création Route
aws ec2 create-route --route-table-id rtb-052bf47049505554f --destination-cidr-block 0.0.0.0/0 --gateway-id igw-05d3ce61881a91e6a

# Association de la Table de Routage à la Subnet
aws ec2 associate-route-table --route-table-id rtb-052bf47049505554f --subnet-id subnet-0561dcb3070c008c8


VPC 2 :


# Création VPC2
aws ec2 create-vpc --cidr-block 172.31.0.0/16 --query Vpc.VpcId --output text

# Tag VPC2
aws ec2 create-tags --resources vpc-08797c0cba497c1d3 --tags Key=Name,Value=lilo-vpc2-cli

# Création Subnet Private
aws ec2 create-subnet --vpc-id vpc-08797c0cba497c1d3 --cidr-block 172.31.1.0/24 --availability-zone us-east-1a --query Subnet.SubnetId --output text

# Tag Subnet Private
aws ec2 create-tags --resources subnet-011d691089eab90e5 --tags Key=Name,Value=lilo-subnet-private-vpc2

# Création Internet Gateway
aws ec2 create-internet-gateway --query InternetGateway.InternetGatewayId --output text

# Attacher la Gateway au VPC
aws ec2 attach-internet-gateway --vpc-id vpc-08797c0cba497c1d3 --internet-gateway-id igw-0602245a28d6707f1

# Création Table de Routage
aws ec2 create-route-table --vpc-id vpc-08797c0cba497c1d3 --query RouteTable.RouteTableId --output text

# Tag Table de Routage
aws ec2 create-tags --resources rtb-0d8e7fdf38aa8b9e1 --tags Key=Name,Value=lilo-rtb-vpc2

# Création Route
aws ec2 create-route --route-table-id rtb-0d8e7fdf38aa8b9e1 --destination-cidr-block 0.0.0.0/0 --gateway-id igw-0602245a28d6707f1

# Association de la Table de Routage à la Subnet
aws ec2 associate-route-table --route-table-id rtb-0d8e7fdf38aa8b9e1 --subnet-id subnet-011d691089eab90e5

# Création Groupe de Sécurité
aws ec2 create-security-group --group-name lilogroupcli2 --description "Groupe de securite via cli" --vpc-id vpc-08797c0cba497c1d3

# Tag Groupe de Sécurité
aws ec2 create-tags --resources sg-06823e7c163fbfd40 --tags Key=Name,Value=lilo-sg-vpc2

# Autorisation Port 22
aws ec2 authorize-security-group-ingress --group-id sg-06823e7c163fbfd40 --protocol tcp --port 22 --cidr 0.0.0.0/0

# Autorisation Port 80
aws ec2 authorize-security-group-ingress --group-id sg-06823e7c163fbfd40 --protocol tcp --port 80 --cidr 0.0.0.0/0


VPC 3 : 

# Création VPC3
aws ec2 create-vpc --cidr-block 20.0.0.0/16 --query Vpc.VpcId --output text

# Tag VPC3
aws ec2 create-tags --resources vpc-0ce83e5d3bacdc64c --tags Key=Name,Value=lilo-vpc3-cli

# Création Subnet Private
aws ec2 create-subnet --vpc-id vpc-0ce83e5d3bacdc64c --cidr-block 20.0.1.0/24 --availability-zone us-east-1a --query Subnet.SubnetId --output text

# Tag Subnet Private
aws ec2 create-tags --resources subnet-099489ca19d8540c9 --tags Key=Name,Value=lilo-subnet-private-vpc3

# Création Internet Gateway
aws ec2 create-internet-gateway --query InternetGateway.InternetGatewayId --output text

# Attacher la Gateway au VPC
aws ec2 attach-internet-gateway --vpc-id vpc-0ce83e5d3bacdc64c --internet-gateway-id igw-0f7918bec9b89b5eb

# Création Table de Routage
aws ec2 create-route-table --vpc-id vpc-0ce83e5d3bacdc64c --query RouteTable.RouteTableId --output text

# Tag Table de Routage
aws ec2 create-tags --resources rtb-035a64adf6e77665f --tags Key=Name,Value=lilo-rtb-vpc3

# Création Route
aws ec2 create-route --route-table-id rtb-035a64adf6e77665f --destination-cidr-block 0.0.0.0/0 --gateway-id igw-0f7918bec9b89b5eb

# Association de la Table de Routage à la Subnet
aws ec2 associate-route-table --route-table-id rtb-035a64adf6e77665f --subnet-id subnet-099489ca19d8540c9

# Création Groupe de Sécurité
aws ec2 create-security-group --group-name lilogroupcli3 --description "Groupe de securite via cli" --vpc-id vpc-0ce83e5d3bacdc64c

# Tag Groupe de Sécurité
aws ec2 create-tags --resources sg-04e1f532d02d433ad --tags Key=Name,Value=lilo-sg-vpc3

# Autorisation Port 80
aws ec2 authorize-security-group-ingress --group-id sg-04e1f532d02d433ad --protocol tcp --port 80 --cidr 0.0.0.0/0

# Autorisation Port 22
aws ec2 authorize-security-group-ingress --group-id sg-04e1f532d02d433ad --protocol tcp --port 22 --cidr 0.0.0.0/0


Instances :


# Création Instance VM1 VPC1
aws ec2 run-instances --image-id ami-0c7217cdde317cfec --count 1 --instance-type t2.micro --key-name mykeylb --security-group-ids sg-00619b47ec1ff00c4 --subnet-id subnet-0561dcb3070c008c8

# Tag Instance VM1 VPC1
aws ec2 create-tags --resources i-04528ef937903ecc4 --tags Key=Name,Value=lilo-vm-nginx-vpc1

# Création Instance VM2 VPC2
aws ec2 run-instances --image-id ami-0c7217cdde317cfec --count 1 --instance-type t2.micro --key-name mykeylb --security-group-ids sg-06823e7c163fbfd40 --subnet-id subnet-011d691089eab90e5

# Tag Instance VM2 VPC2
aws ec2 create-tags --resources i-05671f37f62bbcb5f --tags Key=Name,Value=lilo-vm2-vpc2

# Création Instance VM3 VPC3
aws ec2 run-instances --image-id ami-0c7217cdde317cfec --count 1 --instance-type t2.micro --key-name mykeylb --security-group-ids sg-04e1f532d02d433ad --subnet-id subnet-099489ca19d8540c9

# Tag Instance VM3 VPC3
aws ec2 create-tags --resources i-0f7004d7b12e9b905 --tags Key=Name,Value=lilo-vm3-vpc3

# Bastion : 
ssh -i .ssh/mykeylb.pem -t ubuntu@18.233.150.123 ssh -i .ssh/mykeylb ubuntu@20.0.1.77 ssh -i .ssh/mykeylb ubuntu@172.31.1.146


Nginx Ubuntu : 


# Installation de Nginx
sudo apt update
sudo apt install nginx

# Démarrer le service Nginx
sudo systemctl start nginx

# Activer le démarrage automatique de Nginx au démarrage du système
sudo systemctl enable nginx

# Création du contenu HTML
sudo nano /var/www/html/index.html

# index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Nginx Site</title>
</head>
<body>
    <h1>Welcome to my Nginx site!</h1>
    <p>This is a simple HTML page served by Nginx on Ubuntu.</p>
    <!-- Add a clickable link -->
    <a href="http://lilo-mybucket-vpc1.s3-website-us-east-1.amazonaws.com" target="_blank">Visit My AWS S3 Website</a>
</body>
</html>

# Configuration du serveur virtuel Nginx
sudo nano /etc/nginx/sites-available/default

# Vérifier la syntaxe de la configuration Nginx
sudo nginx -t

# Redémarrer le service Nginx
sudo systemctl restart nginx


Peering (ne pas oublier de modifier dans la table de routage les routes, destination du vpc, cible : connexion d'apperage avec l'ID : pcX-xiiix) : 


# Création de la connexion de peering de VPC1 à VPC2
aws ec2 create-vpc-peering-connection --vpc-id vpc-0738142f5375712ec --peer-vpc-id vpc-08797c0cba497c1d3

# Résultat commande
VpcPeeringConnection:
  AccepterVpcInfo:
    OwnerId: '336749236319'
    Region: us-east-1
    VpcId: vpc-08797c0cba497c1d3
  ExpirationTime: '2024-01-12T15:38:09+00:00'
  RequesterVpcInfo:
    CidrBlock: 10.0.0.0/16
    OwnerId: '336749236319'
    Region: us-east-1
    VpcId: vpc-0738142f5375712ec
  Status:
    Code: initiating-request
    Message: Initiating Request to 336749236319
  VpcPeeringConnectionId: pcx-0beb661d5e6b63867

# Création de la connexion de peering de VPC1 à VPC3
aws ec2 create-vpc-peering-connection --vpc-id vpc-0738142f5375712ec --peer-vpc-id vpc-0ce83e5d3bacdc64c

# Résultat commande
VpcPeeringConnection:
  AccepterVpcInfo:
    OwnerId: '336749236319'
    Region: us-east-1
    VpcId: vpc-0ce83e5d3bacdc64c
  ExpirationTime: '2024-01-12T15:54:40+00:00'
  RequesterVpcInfo:
    CidrBlock: 10.0.0.0/16
    OwnerId: '336749236319'
    Region: us-east-1
    VpcId: vpc-0738142f5375712ec
  Status:
    Code: initiating-request
    Message: Initiating Request to 336749236319
  VpcPeeringConnectionId: pcx-079393ba99985c5bb


# Nous sommmes heureux de vous informer que le projet a été mené à terme avec succès. Toutes les étapes ont été complétées, les configurations sont en place, et le système est opérationnel. Merci pour votre encadrement tout au long du projet.

