<!SLIDE>
# Synchronous Tuning
* Inbound handled by PSAPPSRV on servers in integrationGateway.properties
* Outbound handled by any PSAPPSRV process
* Tune the number of application servers
* Limit will be determined by database table locking

<!SLIDE small>
#integrationGateway.properties
    @@@ ini
    ig.isc.HCMPRD.serverURL=//phcmapp04.prod.cu.edu:9033,//phcmapp05.prod.cu.edu:9033
    ig.isc.HCMPRD.userid=CU_IBUSER
    ig.isc.HCMPRD.password={V1.1}I69UZeBy2134E+zLQYXYxA==
    ig.isc.HCMPRD.toolsRel=8.55.11
    ig.isc.HCMPRD.DomainConnectionPwd={V1.1}cAZUye0Lbx49Zl/GGpVFgQ==
    
    ...
    
    # The following are the Gateway Log Levels
    #   Level                      Value
    #   -------------------------- -----
    #   SUPPRESS ANY LOGGING        -100 {Suppresses any Message Logs}
    #   LANGUAGE_EXCEPTION          -1   {Logs language exceptions only}
    #   STANDARD_GATEWAY_EXCEPTION   1   {Logs language and standard}
    #   WARNING                      2   {Logs all errors & warnings. (Default)}
    #   IMPORTANT_INFORMATION        3   {Logs errors,warnings and important Information}
    #   STANDARD_INFORMATION         4   {Logs errors,warnings, important and standard information}
    #   LOW_IMPORTANCE_INFORMATION   5   {Logs errors,warnings important, standard and low importance information}
    #
    ig.log.level=3
    
    ...
    
    # Profile Information
    # Set it to either TRUE or FALSE
    
    ig.ProfileInformation=TRUE


