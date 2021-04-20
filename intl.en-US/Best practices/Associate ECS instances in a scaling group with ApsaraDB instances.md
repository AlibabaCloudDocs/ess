# Associate ECS instances in a scaling group with ApsaraDB instances

This topic describes how to associate ECS instances in a scaling group with ApsaraDB instances. You can add the ECS instances and the ApsaraDB instances to the same security group, associate the scaling group with the ApsaraDB instances, and add the ECS instances to the whitelists of the ApsaraDB instances.

ECS instances in a scaling group may be automatically released. Therefore, we recommend that you save your application data to ApsaraDB instances. The console is used in this example to demonstrate how to associate ECS instances in a scaling group with ApsaraDB instances.

## Method 1: \(Recommended\) Add an ECS instance and an ApsaraDB instance to the same security group

When a scaling group and an ApsaraDB instance are of the VPC type and added to the same security group, ECS instances in the scaling group can directly access the ApsaraDB instance.

**Note:** This method applies to all ApsaraDB services such as ApsaraDB RDS and ApsaraDB for MongoDB.

In this example, ApsaraDB RDS for MySQL is used. You can perform the following operations:

-   Create a scaling group and an ApsaraDB RDS for MySQL instance:
    1.  Create a VPC-type scaling group. For more information, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).
    2.  Create and enable a scaling configuration whose security group belongs to the same VPC as the scaling group. For more information, see [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md).
    3.  Enable the scaling group. For more information, see [Enable a scaling group](/intl.en-US/Scaling Group/Scaling group/Enable a scaling group.md).
    4.  Create and use an ApsaraDB RDS for MySQL instance whose network type and security group are the same as those of the scaling group. For more information, see [Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md) and [Configure a security group for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Set the whitelist/Configure a security group for an ApsaraDB RDS for MySQL instance.md).

        **Note:** For more information, see [General workflow to use RDS for MySQL](/intl.en-US/RDS MySQL Database/Quick start/General workflow to use RDS for MySQL.md).

-   Modify the scaling group and the ApsaraDB RDS for MySQL instance. Perform the following operations to configure the network type and security group of the ApsaraDB RDS for MySQL instance based on the configurations of the scaling group:
    1.  View the network type of the scaling group and the security group specified in the scaling configuration. For more information, see [t2046971.md\#]().

        **Note:** The network type of a scaling group cannot be changed after the scaling group is created. If the network type of a scaling group is classic network, you must create another scaling group. For more information, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).

    2.  Check whether the network type of the ApsaraDB RDS for MySQL instance is the same as that of the scaling group. If not, change the network type of the ApsaraDB RDS for MySQL instance. For more information, see [Change the network type of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/Change the network type of an ApsaraDB RDS for MySQL instance.md).
    3.  Check whether the security group of the ApsaraDB RDS for MySQL instance is the same as that of the scaling group. If not, change the security group of the ApsaraDB RDS for MySQL instance. For more information, see [Configure a security group for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Set the whitelist/Configure a security group for an ApsaraDB RDS for MySQL instance.md).

## Method 2: Associate a scaling group with an ApsaraDB instance

When you create or modify a scaling group, you can associate it with an ApsaraDB RDS instance. After the scaling group is associated with an ApsaraDB RDS instance, all ECS instances in the scaling group can directly access the ApsaraDB RDS instance, regardless of the network type of the scaling group and the ApsaraDB RDS instance.

**Note:** This method applies only to ApsaraDB RDS.

-   Create a scaling group. For more information, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).
-   Modify the scaling group. For more information, see [Modify a scaling group](/intl.en-US/Scaling Group/Scaling group/Modify a scaling group.md).

    **Note:** If ECS instances exist in a scaling group, you can use the following method to add the instances to the whitelists of the associated ApsaraDB RDS instances when you modify the scaling group:

    -   Console: In the **Edit Scaling Group** dialog box, select **Add or remove instances in the scaling group to or from whitelists of RDS instances when you associate or disassociate RDS instances**.
    -   [AttachDBInstances](/intl.en-US/API Reference/Scaling group/AttachDBInstances.md): Set ForceAttach to true.

## Method 3: Use lifecycle hooks and OOS templates to add ECS instances to the whitelists of ApsaraDB instances

You can use lifecycle hooks in conjunction with Operation Orchestration Service \(OOS\) templates to put ECS instances in a scaling group into the wait state. Then, you can add the ECS instances to the whitelists of ApsaraDB instances associated with the scaling group. After the ECS instances are added to the whitelists of the ApsaraDB instances, the ECS instances can directly access the ApsaraDB instances, regardless of the network type of the scaling group and the ApsaraDB instances.

**Note:** This method applies only to PolarDB, ApsaraDB for MongoDB, AnalyticDB for PostgreSQL, and AnalyticDB for MySQL.

-   [Automatically add or remove ECS instances to or from the whitelist of a PolarDB cluster]()
-   [Automatically add or remove ECS instances to or from the whitelist of a MongoDB instance]()
-   [Automatically add or remove ECS instances to or from the whitelist of an AnalyticDB for MySQL cluster]()

