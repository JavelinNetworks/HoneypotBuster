### Microsoft PowerShell module designed for red teams that can be used to find honeypots and honeytokens in the network or at the host.

## CodeExecution

**Execute code on a target machine using Import-Module.**


## `Invoke-HoneypotBuster`

HoneypotBuster is a tool designed to spot Honey Tokens, Honey Bread Crumbs, and Honey Pots used by common Distributed Deception vendors. This tool will help spot the following deception techniques:

#### 1. Kerberoasting Service Accounts Honey Tokens
Just like the one described in the ADSecurity article by Sean Metcalf, this tricks attackers to scan for Domain Users with assigned SPN (Service Principal Name) and {adminCount = 1} LDAP Attribute flag. So when you try to request TGS for that user, you’ll be exposed as Kerberoasting attempt. TGS definition: A ticket granting server (TGS) is a logical key distribution center (KDC) component that is used by the Kerberos protocol as a trusted third party.

#### 2. Fake Computer Accounts Honey Pots
Creating many domain computer objects with no actual devices associated to them will result in confusion to any attacker trying to study the network. Any attempt to perform lateral movement into these fake objects will lead to exposure of the attacker.


#### 3. Fake Credentials Manager Credentials Breadcrumbs 
Many deception vendors are injecting fake credentials into the “Credentials Manager”. These credentials will also be revealed using tools such as Mimikatz. Although they aren’t real, attackers might confuse them as authentic credentials and use them.


#### 4. Fake Domain Admins Accounts Honey Tokens 
Creating several domain admins and their credentials who have never been active is bad policy. These Honey Tokens lure attackers to try brute-forcing domain admin credentials. Once someone tries to authenticate to this user, an alarm will be triggered, and the attacker will be revealed. Microsoft ATA uses this method.


#### 5. Fake Mapped Drives Breadcrumbs 
Many malicious automated scripts and worms are spreading via SMB Shares, especially if they’re mapped as Network Drive Share. This tool will try to correlate some of the data collected before to identify any mapped drive related to a specific Honey Pot server.


#### 6. DNS Records Manipulation HoneyPots 
One of the methods deception vendors use to detect fake endpoints is registering their DNS records towards the Honey Pot Server. They will then be able to point the attacker directly to their honey pot instead of actual endpoints.


## License

The Honeypot buster project and all individual scripts are under the [BSD 3-Clause license] unless explicitly noted otherwise.

## Usage

To install any of these modules, drop the powershell scripts into a directory and type `Import-Module PathTo\scriptName.ps1`

Then run the Module from the Powershell.

Refer to the comment-based help in each individual script for detailed usage information.
