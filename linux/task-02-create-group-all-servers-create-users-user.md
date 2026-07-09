# Task 02 create-group-all-servers-create-users-user

The system admin team at xFusionCorp Industries has streamlined access management by implementing group-based access control. Here's what you need to do:

a. Create a group named nautilus_developers across all App servers within the Stratos Datacenter.

b. Add the user rajesh into the nautilus_developers group on all App servers. If the user doesn't exist, create it as well.


ssh user@host para alternar entre os servers

groupadd para adicionar grupo nautilus_developers

getent group nautilus_developers para ver se criou o grupo, ou
grep nautilus_developers /etc/group

useradd -G nautilus_developers rajesh