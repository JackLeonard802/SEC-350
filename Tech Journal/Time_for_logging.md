# How to Standardize Time Settings for Logging

## Linux
* `sudo vi /etc/rsyslog.conf`
* Comment out the line that starts with `$ActionFileDefaultTemplate RSYSLog_TraditionalFileFormat`
* If the wording isn't exact, check for a description that talks about standard timestamps/timezones
