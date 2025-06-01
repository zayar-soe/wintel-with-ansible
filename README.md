# 🔧 Windows Patch Management with Ansible (Lenovo Wintel Servers)

This repository automates the **security patching lifecycle** for Lenovo Windows (Wintel) servers using **Ansible and WinRM**. It includes a modular four-step approach to **check, approve, apply, and notify** patching tasks through Ansible playbooks.

---
Requirements
Ansible 2.15+

Python with pywinrm installed

WinRM enabled on Windows servers

Email (SMTP) server for notifications

Enable WinRM on Target Windows Servers
On each Windows server, run the following PowerShell commands:

winrm quickconfig -force
winrm set winrm/config/service '@{AllowUnencrypted="true"}'
winrm set winrm/config/service/auth '@{Basic="true"}'
Set-Item WSMan:\localhost\Client\TrustedHosts -Value "*" -Force

You may also need to allow TCP port 5985 through the firewall.

📜 Playbook Workflow
✅ 1. Check for Available Security Patches

ansible-playbook check_for_patches.yml
Scans the Wintel servers for SecurityUpdates and outputs available patches.

📧 2. Send Approval Email

ansible-playbook request_approval.yml
Sends an email to approval_email requesting authorization to proceed with patching.

⚙️ 3. Apply Patches and Reboot

ansible-playbook apply_patch.yml
Installs all security updates on the servers and reboots if required.

📤 4. Notify Completion

ansible-playbook notify_result.yml
Sends a summary email confirming that patching has been completed successfully.
