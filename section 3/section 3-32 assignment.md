# Section 3-32 Assignment

## The Assignment

### Objective

- Use different Linux distro containers to check curl cli tool version
- Use two different terminal windows to start bash in both centos:7 and ubuntu:14.04 using -it
- Learn docker container --rm option to save cleanup
- Ensure curl is installed and on latest version for that distro

### Notes

- Update curl commands:
  - Ubuntu:
    - apt-get update && apt-get install curl
  - CentOS:
    - yum update curl
- Check curl version:
  - curl --version

## Solution

### Commands

- Ubuntu System:
  1. docker container run --name ubuntu -it --rm ubuntu:14.04 bash
  1. apt-get update && apt-get install curl
  1. curl --version
    - Response:
      - curl 7.35.0 (x86_64-pc-linux-gnu) libcurl/7.35.0 OpenSSL/1.0.1f zlib/1.2.8 libidn/1.28 librtmp/2.3
      Protocols: dict file ftp ftps gopher http https imap imaps ldap ldaps pop3 pop3s rtmp rtsp smtp smtps telnet tftp 
Features: AsynchDNS GSS-Negotiate IDN IPv6 Largefile NTLM NTLM_WB SSL libz TLS-SRP
  1. exit

- CentOS System:
  1. docker container run --name centos -it --rm centos:7 bash
  1. yum update curl
  1. curl --version
    - Response:
      - curl 7.29.0 (x86_64-redhat-linux-gnu) libcurl/7.29.0 NSS/3.36 zlib/1.2.7 libidn/1.28 libssh2/1.4.3
      Protocols: dict file ftp ftps gopher http https imap imaps ldap ldaps pop3 pop3s rtsp scp sftp smtp smtps telnet tftp 
  1. exit

- final command (to verify everything is removed)
  - docker container ls -a