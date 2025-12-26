## Server-Agent Connection Troubleshotting

Sometimes the lab can take hours to set up successfully. Do not give up — keep trying.
When working on a Wazuh home lab, it’s common to face connection issues between the server and the agent. Troubleshooting these issues helps you gain a deeper understanding of how the system works.

One of the most common problems happens when you return to your lab after a few days. Even though the Wazuh server and agent were connected before, they may appear disconnected.

## Common checks on the Wazuh server

First, check the status of the following services on the server:

            sudo systemctl status wazuh-manager
            sudo systemctl status wazuh-indexer
            sudo systemctl status wazuh-dashboard

If any of them are not running, restart them:

            sudo systemctl restart wazuh-manager
            sudo systemctl restart wazuh-indexer
            sudo systemctl restart wazuh-dashboard

## Common checks on the Wazuh agent
On the agent machine, check whether the agent service is running:

            sudo systemctl status wazuh-agent

If it is not running, start and enable it:

            sudo systemctl start wazuh-agent
            sudo systemctl enable wazuh-agent

## Server IP address change (very common issue)
Check the current IP address of the Wazuh server and note it down.

On the agent machine, open the configuration file:

            sudo nano /var/ossec/etc/ossec.conf


Update the following line with the correct server IP address:

            <address>WAZUH_SERVER_IP</address>


Save the file, then restart the agent:

            sudo systemctl stop wazuh-agent
            sudo systemctl restart wazuh-agent

In most cases, these steps will resolve the server and agent connection issue.

