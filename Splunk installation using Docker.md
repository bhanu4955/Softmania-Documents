Installation Guide for Splunk using Docker
Step 1: Install Docker in Linux Environment
To set up Docker on your Linux environment, follow these commands:
```
sudo apt update
sudo apt install -y docker.io
```

Command Breakdown:

sudo apt update: Updates the package list to the latest version.

sudo apt install -y docker.io: Installs Docker on your Linux system.

Note:
Ensure that you have administrative privileges (sudo) for the installation.

Step 2: Checking Docker Installation

To verify whether Docker is installed on your system, use the following command:
```
docker --version
```

Step 3: Installing Splunk

Execute the following command to install Splunk using Docker:
```
docker run --name splunk1 -p 8000:8000 -e "SPLUNK_PASSWORD=*****" -e "SPLUNK_START_ARGS=--accept-license" -it splunk/splunk:latest
```
Explanation of the command:
run: Creates and runs the container.

--name container Name : Assigns the name to the container.

-p 8000:8000: Port Mapping(The default port number for Splunk is set to 8000.)

-e "SPLUNK_PASSWORD=*****": Sets the Splunk admin password(-e : environment variables)

-e "SPLUNK_START_ARGS=--accept-license": Accepts the Splunk license.

-it: Opens an interactive terminal in the container.

splunk/splunk:latest: Pulls the latest Splunk image from the Docker registry.

The installation process may take some time. Once completed, you will see a screen resembling.

Step 3: Confirmation of Splunk Installation

Upon successful installation, access the Splunk interface by entering the IP address and port number (Ip Address:8000)in your web browser.
