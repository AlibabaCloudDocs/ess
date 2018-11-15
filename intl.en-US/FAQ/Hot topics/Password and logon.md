# Password and logon {#concept_25968_zh .concept}

## When Auto Scaling automatically creates instances, how do I view their passwords and subsequently log on to these instances? {#section_ojw_dfl_sfb .section}

-   Instances automatically created by Auto Scaling do not have the same password. In a Linux environment, we recommend that you set a public/private key certificate for SSH logon without password.
-   If you do not want to set a public/private key certificate for SSH logon without password, you must reset the password on the console, and then restart the instance to apply the new password, before you can log on.

## Why are the passwords of instances created by Auto Scaling different from the password for my custom image? { .section}

-   Created ECS instances do not have the same password as the custom image. To ensure password security, we recommend that you set a public/private key certificate for SSH password-free logon.
-   If you do not want to set a public/private key certificate for SSH logon without password, you must reset the password on the console, and then restart the instance to apply the new password, before you can log on.

## When using a custom image to generate Linux system instances, can I manage the instances through SSH logon without password? { .section}

1.  You can set a public/private key certificate for SSH logon without password as follows: Establish a public key and private key in the custom image’s ECS server-end instance.
2.  Copy the ECS instance idc.pub to the client.
3.  Delete the public key from the server-end.
4.  Modify the SSH configuration file on the server-end.
5.  Configure the client software.

Take SecureCRT configuration as an example:

1.  Select the corresponding remote connection information.
2.  Right-click on the **Attribute** option
3.  and select **SSH2**.
4.  Clear the **Password** option and select **PublicKey**.
5.  Click the **Attribute** button on the right side
6.  and select **Use Session Public Key Settings**.
7.  Select **Use ID or Certificate File**, and **idc.pub** \(the public and private key files you previously copied from the server\).

