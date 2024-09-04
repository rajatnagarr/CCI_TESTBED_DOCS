Launching OpenStack Instances with USRP Access
==============================================

This documentation provides steps to create and launch OpenStack instances with USRP (Universal Software Radio Peripheral) access, either through the Command-Line Interface (CLI) or the OpenStack dashboard.

Keywords: USRP, Instance, OpenStack, CLI, Cloud Computing

.. note::
    - Each USRP can only be connected to one instance at a time.
    - Users cannot create an instance with a USRP network unless granted access by an OpenStack admin.
    - This guide is intended for users on Linux and MacOS devices.

CLI Instructions
----------------

To create an OpenStack instance with USRP access using the Command-Line Interface (CLI), follow the steps below:

1. **Download Your OpenStack RC File**
   
   - Log in to the OpenStack portal: `https://portal.ccixgtestbed.org/auth/login`.
   - Download your profile's RC file from the drop-down in the top-right corner.

   .. image:: https://prod-files-secure.s3.us-west-2.amazonaws.com/9a7748d3-234c-4b98-8771-4fd63af649c0/54587d96-9627-4747-8e16-2d01520c307c/Untitled_design.gif

2. **Install Necessary Dependencies**

   Install the required packages on your device:
   
   .. code-block:: bash

       sudo apt update
       sudo apt install -y python3-pip python3-dev
       sudo pip3 install --upgrade pip
       sudo pip3 install python-openstackclient

3. **Source the OpenStack RC File**

   Navigate to the directory where you downloaded the RC file and source it:
   
   .. code-block:: bash

       . <rc_file_name>.sh

   This command will prompt you to enter your OpenStack password.

4. **Create an Instance with USRP Access**

   Use the following command to create an instance with USRP access:
   
   .. code-block:: bash

       openstack server create --flavor <flavor_name> --image <image_name> --nic port-id=$(openstack port list | grep <usrp_number> | awk '{print $2}') --nic net-id=<internal_network_id> --availability-zone radio <instance_name>

   **Note**: Replace `<flavor_name>`, `<image_name>`, `<usrp_number>`, `<internal_network_id>`, and `<instance_name>` with the appropriate values.

   For further details, watch the tutorial video: https://youtu.be/NtC79iuUNNI

Dashboard Instructions
----------------------

To create an OpenStack instance with USRP access using the OpenStack dashboard, follow these steps:

1. **Log in to the OpenStack Dashboard**

   - Access the OpenStack portal: `https://portal.ccixgtestbed.org/auth/login`.
   - Navigate to the "Launch Instance" screen under the project section.

2. **Configure Instance Settings**

   - Provide a name for the instance.
   - Select `radio` as the availability zone (do not use `compute`).
   - Choose the boot source (e.g., `Ubuntu-20.04-ServerImage`).
   - Attach the appropriate USRP port to the instance.

   .. image:: https://cci-xg-testbed-cci-testbed-docs.readthedocs-hosted.com/en/latest/_images/launchInstance.png

3. **Launch the Instance**

   After configuring the settings, click the **Launch Instance** button to provision the instance with USRP access.

.. note::
    If you encounter any issues with the OpenStack dashboard, login credentials, or USRP port access, raise a ticket in Redmine or contact the administrator at `cci.xg.testbed.admin@cyberinitiative.org`.
