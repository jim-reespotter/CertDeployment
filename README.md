# CertDeployment

A tool for pulling and distributing certificates

## The issue:
Organisations use certificates in a range of situations. The creation and deployment of various types of certificate may to some extent be managed by on internal CA (such as Active Directory Certificate Services), but this still leaves the issue of deploying publicly signed certificates from an external CA. There are tools for dealing with this on a per-server basis (such as CertBot ACME client) but it would be beneficial to have a centralised service to manage this. In addition, configuring CertBot to work in the variety of situations these certs are deployed is challenging.

Public server certificates could be used in various situations, including the following:
- Webservers
  - Windows (IIS)
  - Linux (Apache, NGinx, Lighttpd)
  - Java (Tomcat, Jetty)
- LDAP servers
  - Active Directory
  - OpenLDAP
- RADIUS servers
  - NPS
  - FreeRadius
  - Proprietory/appliance based: Clearpass/ISE/Khipu
- Loadbalancers
  - Kemp, Fortigate, Palo, Barracuda

With the announcement from Google of shortening the acceptable validity period of publicly accepted HTTPS server certs to 3 months, the work required to keep these certificates up to date has increased.

## Proposed solution:

Build a centralised service to:
- pull updated certificates from the external CA
- push these updated certificates to the necessary situations listed above

To simplify this, the following constraints are proposed:
- Only deal with re-issues of certificates (issued from same CSR, so private key will not change)
- assume the signing chain remains unchanged
