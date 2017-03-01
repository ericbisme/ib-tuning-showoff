<!SLIDE>
# Synchronous Statistics
* Enable at:
  * integrationGateway.properties
  * Integration Broker > Configuration > System Setup Options
* Timings for all SYNC messages
* Have an Archiving Plan
  * PIA page becomes unresponsive
  * Stats can be queried via SQL

<!SLIDE small>
#integrationGateway.properties
    @@@ ini
    ig.isc.HCMPRD.serverURL=//server.cu.edu:9033,//server.cu.edu:9033
    ig.isc.HCMPRD.userid=IBUSER
    ig.isc.HCMPRD.password={V1.1}IlkjljEr89fEE+zLQYXYxA==
    ig.isc.HCMPRD.toolsRel=8.55.11
    ig.isc.HCMPRD.DomainConnectionPwd={V1.1}dWEnvroi8902Fl/GGpVFgQ==
    
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
