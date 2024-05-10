---
title: "Windows as Ansible Client"
datePublished: Fri May 10 2024 09:26:42 GMT+0000 (Coordinated Universal Time)
cuid: clw0h3lvz000e08mf8ke0h1ys
slug: windows-as-ansible-client

---

Ansible Installation on ubuntu \[[LINK](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu)\] Follow the link

Window as Ansible Client

Step1: Create Certificate

```powershell
New-SelfSignedCertificate -DnsName "DNS Name" -CertStoreLocation Cert:\LocalMachine\My
```

STEP2: Create HTTPS Listener

```powershell
winrm create winrm/config/Listener?Address=*+Transport=HTTPS '@{Hostname="DNS Name"; CertificateThumbprint="ThumbPrint"}'
```

Windows server's local firewall to allow incoming TCP traffic on port 5986. This ensures that the traffic is allowed both at the AWS security group level (5986 and 5985) and at the Windows server's firewall level, thus enabling WinRM over HTTPS communication to the server.

```powershell
netsh advfirewall firewall add rule name="Windows Remote Management (HTTPS-In)" dir=in action=allow protocol=TCP localport=5986
```

Make sure the Basic Auth is set to true, if not then execute below commands.

```powershell
Set-Item -Force WSMan:\localhost\Service\auth\Basic $true
```

Check The Service

```powershell
winrm get winrm/config
```

Ansible Inventory file

```yaml
[win]
172.16.0.67

[win:vars]
ansible_user=Admin
ansible_password=Admin
ansible_port=5986
ansible_connection=winrm
ansible_winrm_server_cert_validation=ignore
ansible_winrm_transport=basic
```

Thank You