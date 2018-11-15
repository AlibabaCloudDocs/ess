# Monitoring and automation {#concept_25971_zh .concept}

## How does Auto Scaling determine if its ECS instances are available? {#section_hj3_cxk_sfb .section}

If the Server Load Balancer is available in the expected Auto Scaling group, it will check that the ports of the backend ECS instances are functional before forwarding requests to the ECS instances.

## What are the triggering conditions for Auto Scaling alarms? { .section}

Monitoring alarms in Auto Scaling are triggered based on the CPU load, memory usage, average system load, and Internet and intranet inbound and outbound traffic. These are used to automatically increase or decrease the number of ECS instances.

## Can Auto Scaling support dynamic scaling based on custom alarms in CloudMonitor? { .section}

No. Dynamic scaling based on custom monitoring settings is not supported.

## How can I automate the deployment of the ECS applications created in a scaling group? { .section}

To automatically install or update a program, or automatically load code after an ECS instance is automatically created in a scaling group, you must store an execution script in a custom image and set up a command to automatically run this script upon operating system startup.

**Note:** CentOs 6 and lower systems use system V init as the initialization process, and CentOs 7 uses systemd for the initialization process. Their working principles are quite different. Descriptions about CentOs 6 and CentOs 7 are as follows.

## For CentOs 6 and lower systems, { .section}

1.  create the following shell test script:

    ```
    #. /bin/sh
    # chkconfig: 6 10 90
    # description: Test Service
    echo "hello world!"
    
    ```

    The `# chkconfig: 6 10 90` in the preceding script is described as follows:

    In the preceding output, 6 is the default start level. There are a total of 7 levels ranging from 0-6. Level 0: Shutdown. Level 1: Single user mode. Level 2: Multiuser command line mode with no network connection. Level 3: Multiuser command line mode with network connection. Level 4: Unavailable. Level 5: Multiuser mode with graphic interface. Level 6: Restart . 10 is the start priority and 90 is the stop priority. The priority range is 0-100. The higher the number, the lower the priority.

2.  Put the test file in the /etc/rc.d/init.d/ directory and run `chkconfig --level 6 test on`.

    **Note:** This test script will run each time the system starts up.

    Example

    The following example shows how to use a script to install Phpwind. Put the Phpwind installer in the script for execution \(you will need to enter the database password\). An example output is as follows:

    ```
    cd /tmp
    echo "phpwind"
    yum install -y \
    unzip \
    wget \
    httpd \
    php \
    php-fpm \
    php-mysql \
    php-mbstring \
    php-xml \
    php-gd \
    php-pear \
    php-devel
    chkconfig php-fpm on \
    && chkconfig httpd on
    wget http://pwfiles.oss-cn-hangzhou.aliyuncs.com/com/soft/phpwind_v9.0_utf8.zip \
    && unzip -d pw phpwind_v9.0_utf8.zip \
    && mv pw/phpwind_v9.0_utf8/upload/* /var/www/html \
    && wget http://ess.oss-cn-hangzhou.aliyuncs.com/ossupload_utf8.zip -O ossupload_utf8.zip \
    && unzip -d ossupload ossupload_utf8.zip \
    && /bin/cp -rf ossupload/ossupload_utf8/* /var/www/html/src/extensions/ \
    && chown -R apache:apache /var/www/html
    service httpd start && service php-fpm start
    echo "Install CloudMonitor"
    wget http://update2.aegis.aliyun.com/download/quartz_install.sh
    chmod +x quartz_install.sh
    bash quartz_install.sh
    echo "Installation complete"
    ```


## CentOs 7 system: { .section}

CentOs 7 uses systemd for the initialization process, and the working principle is quite different from system V init. Assume that you have created the script and it is running correctly. Follow these steps to run the script at system shutdown when you use systemd.

1.  Create a file run-script-when-shutdown.service under /etc/systemd/system, including the following content \(change the value of the variable ExecStop to the absolute path to which you run the script\):

    ```
    [Unit]
    Description=service to run script when shutdown
    After=syslog.target network.target
    
    [Service]
    Type=simple
    ExecStart=/bin/true
    ExecStop=/path/to/script/to/run
    RemainAfterExit=yes
    
    [Install]
    WantedBy=default.target
    ```

2.  Run the following command to enable the newly created service:

    ```
    systemctl enable run-script-when-shutdown
    systemd start run-script-when-shutdown
    ```

    **Note:** 

    -   Run the restart command to make the current service take effect immediately.
    -   You can configure run-script-when-shutdown to run the fixed script. When needed, the relevant personnel can modify the fixed script to make it more flexible and practical.
3.  When you do not need to run the preceding service, run the following command:

    ```
    systemctl disable run-script-when-shutdown
    ```


