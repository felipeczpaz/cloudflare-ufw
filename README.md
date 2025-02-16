# Cloudflare UFW

This repository contains a shell script to configure UFW (Uncomplicated Firewall) on Linux systems to allow traffic from Cloudflare IP addresses. This setup is essential for users who utilize Cloudflare's services and want to ensure their server remains secure while allowing legitimate traffic.

## Prerequisites

- A Linux distribution with UFW installed (most modern distributions have it pre-installed).
- Basic knowledge of using the terminal and executing shell scripts.

## Setup Instructions

1. **Check UFW Status**

Ensure that UFW is not enabled:

```bash
sudo ufw status verbose
```

If UFW is active, disable it:

```bash
sudo ufw disable
```

2. **Reset UFW Rules**

Clear any existing rules:

```bash
sudo ufw reset
```

4. **Set Default Rules**

Set the default rules to deny incoming and allow outgoing connections:
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

4. **Add Essential Rules**

Prevent accidental lockout by adding the following rules: 
```bash
sudo ufw allow from 192.168.1.0/24
sudo ufw allow ssh
```

5. **Enable UFW**

Enable the firewall: 

```bash
sudo ufw enable
```

Respond with `y` to any prompts regarding existing SSH connections.

6. **Clone the Repository**

Clone this repository to your system: 

```bash
git clone https://github.com/felipeczpaz/cloudflare-ufw.git
```

7. **Run the Script**

Execute the script to download Cloudflare's current IPs and install them into UFW's configuration: 

```bash
sudo /bin/cloudflare-ufw.sh
```

8. **Verify Rules**

Check that the rules have been successfully added: 

```bash
sudo ufw status verbose
```

## Scheduling

To keep your firewall rules up to date, consider running the script weekly. You can automate this using cron:

1. Open the crontab editor: 

```bash
sudo crontab -e
```

2. Add the following line to schedule the script to run every Monday at midnight: 

```bash
0 0 * * 1 /bin/cloudflare-ufw.sh > /dev/null 2>&1
```

## Other UFW Commands

- Delete a Single Rule

To delete a specific rule, first get a numbered list of all rules:

```bash
sudo ufw status numbered
```

Then delete the rule by its number:

```bash
sudo ufw delete <rule_number>
```

## Contributions

Contributions are welcome! If you have suggestions for improvements or new features, please fork the repository and submit a pull request. You can also open an issue to discuss any ideas or report bugs.
