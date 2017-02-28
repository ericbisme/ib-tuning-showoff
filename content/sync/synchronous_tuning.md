<!SLIDE>
# Synchronous Tuning
* Inbound handled by PSAPPSRV on servers listed in integrationGateway.properties
* Outbound handled by any PSAPPSRV process
* Adjust the number of PSAPPSRV processes and application servers
* Limit will be determined by database table locking
