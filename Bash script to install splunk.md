```
#!/bin/bash

SPLUNK_FILENAME="splunk-9.2.0.1-d8ae995bf219-Linux-x86_64.tgz"
SPLUNK_URL="https://download.splunk.com/products/splunk/releases/9.2.0.1/linux/${SPLUNK_FILENAME}"
INSTALL_DIR="/opt/splunk"

# Download Splunk
sudo wget -O ${SPLUNK_FILENAME} "$SPLUNK_URL"

# Extract Splunk
sudo tar -xzf ${SPLUNK_FILENAME} -C $INSTALL_DIR --strip-components=1

#permissions
sudo chmod +x ${SPLUNK_FILENAME}

# Start Splunk
sudo $INSTALL_DIR/bin/splunk start --accept-license --answer-yes

# Enable Splunk to start on boot
sudo ${SPLUNK_DIR}/bin/splunk enable boot-start -user splunk

```
