<!SLIDE>
# Dedicated PUBSUB Processes
* Service high volume and/or high priority
* Dedicated queues cannot hold up others
  * Cannot be held up by others
* Tune the number of handlers

<!SLIDE[tpl=none]>
#psadmin - Dedicated Messaging Processes
    @@@ Console nochrome
    ---------------------------------------------------------------
                  Messaging Server Administration menu
    ---------------------------------------------------------------
      Domain Name : <domain>

      In addition to the default messaging servers, the following
      dedicated messaging servers are in the domain configuration:

       SERVER NAME       TYPE  QUEUES
       ----------------  ----  ----------------
       ROLBRK            BRK   ROLESYNCHEXT_CHNL
       ROLPUB            PUB   ROLESYNCHEXT_CHNL
       ROLSUB            SUB   ROLESYNCHEXT_CHNL
       PERBRK            BRK   PERSON_DATA
       PERPUB            PUB   PERSON_DATA
       PERSUB            SUB   PERSON_DATA

      Commands:
       1) Create a new messaging server
       2) Edit the queue list for a messaging server
       3) Delete an existing messaging server
       q) Quit

    Command to execute (1-3, q) :

<!SLIDE>
#shell - Dedicated Messaging Processes
    @@@ Bash
    #!/bin/bash
    psadmin -c addmsgsrv -d hcmprd -s ROLBRK -t BRK ROLESYNCHEXT_CHNL
    psadmin -c addmsgsrv -d hcmprd -s ROLPUB -t PUB ROLESYNCHEXT_CHNL
    psadmin -c addmsgsrv -d hcmprd -s ROLSUB -t SUB ROLESYNCHEXT_CHNL
    psadmin -c addmsgsrv -d hcmprd -s PERBRK -t BRK PERSON_DATA
    psadmin -c addmsgsrv -d hcmprd -s PERPUB -t PUB PERSON_DATA
    psadmin -c addmsgsrv -d hcmprd -s PERSUB -t SUB PERSON_DATA

<!SLIDE small> 
#puppet - Dedicated Messaging Processes
    @@@ Puppet
    # This is a TYPE to create a single dedicated message process on a PeopleSoft appserver
    define ps_dedicated_appmsg::process (
      $type,
      $queue,
      $ps_home_location       = hiera('ps_home_location'),
      $ps_config_home         = hiera('ps_config_home'),
      $domain                 = hiera('appserver_domain_name'),
      $psft_runtime_user_name = hiera('psft_runtime_user_name'),
      $min                    = '2',
      $max                    = '2',
      $scan_interval          = '5',
    ) {
    
      exec { "Add Dedicated Message server ${name} to ${domain}":
        command     => "/usr/bin/su -m -s /bin/bash - ${psft_runtime_user_name} -c \"psadmin -c addmsgsrv -d ${domain} -s ${name} -t ${type} ${queue}\"",
        returns => ["0", "50"],
      }
    
      Ini_setting {
        ensure  => present,
        path    => "${ps_config_home}/appserv/${domain}/psappsrv.cfg",
        section => "PS${type}HND_${name}",
        require => Exec["Add Dedicated Message server ${name} to ${domain}"]
      }
    
      ini_setting { "Setting Min for ${name}":
        setting => 'Min Instances',
        value   => $min,
      }
    
      ini_setting { "Setting Max for ${name}":
        setting => 'Max Instances',
        value   => $max,
      }
    
      ini_setting { "Setting Scan Interval for ${name}":
        section => "PS${type}DSP_${name}",
        setting => 'Scan Interval',
        value   => ${scan_interval},
      }
    }

<!SLIDE>
    @@@ ini
    [PSPUBHND_PERPUB]
    ;===============================================================
    ; Settings for PERPUB publication contract handler
    ;===============================================================
    Min Instances=6
    Max Instances=6
    Service Timeout=1200
    Recycle Count=20000
    ; Dynamic change not allowed for the ProcessRestartMemoryLimit
    ProcessRestartMemoryLimit=0
    Allowed Consec Service Failures=0

