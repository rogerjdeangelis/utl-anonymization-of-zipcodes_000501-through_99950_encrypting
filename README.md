# utl-anonymization-of-zipcodes_000501-through_99950_encrypting
Anonymization of zipcodes_000501 through_99950 
    Anonymization of zipcodes 000501 through 99950                                                           
                                                                                                             
    github                                                                                                   
    https://tinyurl.com/yaw975je                                                                             
    https://github.com/rogerjdeangelis/utl-anonymization-of-zipcodes_000501-through_99950_encrypting         
                                                                                                             
    True anonymization of high dimensional data is extremely difficult.                                      
                                                                                                             
    Since our cadinality is a maximum of 99999 then CRC32 is adequate                                        
                                                                                                             
    Hashes of '9999'                                                                                         
                                                                                                             
    CRC32  : F8C1A4BB                                                                                        
    MD5    : 36678968064D487BB169300312CBCF2B                                                                
    SHA1   : 589205D6D61D7C2F0C8D2F4B29D6DB9ACA3A91D7                                                        
    SHA256 : FEA2EA1F88FF2AB557A8EC16CB7C977886DC2A819430A9615038A9FA922806E3                                
                                                                                                             
                                                                                                             
    related repos (pytho r and SAS                                                                           
    https://tinyurl.com/y9uvq7dc                                                                             
    https://github.com/rogerjdeangelis?tab=repositories&q=encrypt&type=&language=                            
                                                                                                             
    SAS Forum                                                                                                
    https://tinyurl.com/ya7n6g5t                                                                             
    https://communities.sas.com/t5/SAS-Programming/unique-random-Patient-ID/m-p/648204                       
                                                                                                             
    *_                   _                                                                                   
    (_)_ __  _ __  _   _| |_                                                                                 
    | | '_ \| '_ \| | | | __|                                                                                
    | | | | | |_) | |_| | |_                                                                                 
    |_|_| |_| .__/ \__,_|\__|                                                                                
            |_|                                                                                              
    ;                                                                                                        
                                                                                                             
    options validvarname=upcase;                                                                             
    libname sd1 "d:/sd1";                                                                                    
    data have;                                                                                               
       retain zipcode;                                                                                       
       call streaminit(321);                                                                                 
       set sashelp.zipcode(keep=zip x y);                                                                    
       zipcode=put(zip,z5. );                                                                                
       do rep=1 to int(3*rand('uniform'))+1;                                                                 
         keep zipcode x y;                                                                                   
         output;                                                                                             
       end;                                                                                                  
    run;quit;                                                                                                
                                                                                                             
                                                                                                             
    Up to 40 obs WORK.HAVE total obs=82,702                                                                  
                                                                                                             
      Obs    ZIPCODE        X          Y                                                                     
                                                                                                             
        1     00501     -73.0464    40.8131                                                                  
        2     00544     -73.0493    40.8132                                                                  
        3     00544     -73.0493    40.8132                                                                  
        4     00601     -66.7236    18.1660                                                                  
        5     00602     -67.1866    18.3830                                                                  
       ...                                                                                                   
    82699     99929     -132.385    56.4677                                                                  
    82700     99929     -132.385    56.4677                                                                  
    82701     99929     -132.385    56.4677                                                                  
    82702     99950     -131.640    55.3400                                                                  
    ;;;;                                                                                                     
    run;quit;                                                                                                
                                                                                                             
    *            _               _                                                                           
      ___  _   _| |_ _ __  _   _| |_                                                                         
     / _ \| | | | __| '_ \| | | | __|                                                                        
    | (_) | |_| | |_| |_) | |_| | |_                                                                         
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                        
                    |_|                                                                                      
    ;                                                                                                        
                                                                                                             
    WORK.WANT total obs=82,702                                                                               
                                                                                                             
      Obs    ZIPANON     ZIPCODE                  X          Y                                               
                                                                                                             
        1    3B10A688     00501               -73.0464    40.8131                                            
                                                                                                             
        2    2F169703     00544  * same hash  -73.0493    40.8132                                            
        3    2F169703     00544               -73.0493    40.8132                                            
                                                                                                             
        4    395618D1     00601               -66.7236    18.1660                                            
        5    A05F496B     00602               -67.1866    18.3830                                            
                                                                                                             
    82699    7EFF98A7     99929  * same hash  -132.385    56.4677                                            
    82700    7EFF98A7     99929               -132.385    56.4677                                            
    82701    7EFF98A7     99929               -132.385    56.4677                                            
                                                                                                             
    82702    4862B6C4     99950               -131.640    55.3400                                            
                                                                                                             
    *                                                                                                        
     _ __  _ __ ___   ___ ___  ___ ___                                                                       
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                      
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                      
    | .__/|_|  \___/ \___\___||___/___/                                                                      
    |_|                                                                                                      
    ;                                                                                                        
                                                                                                             
    data want;                                                                                               
      length zipanon $32;                                                                                    
      set have;                                                                                              
      zipanon = hashing('crc32',zipcode);                                                                    
    run;quit;                                                                                                
                                                                                                             
    *                                                                                                        
      ___ ___  _ __ ___  _ __   __ _ _ __ ___                                                                
     / __/ _ \| '_ ` _ \| '_ \ / _` | '__/ _ \                                                               
    | (_| (_) | | | | | | |_) | (_| | | |  __/                                                               
     \___\___/|_| |_| |_| .__/ \__,_|_|  \___|                                                               
                        |_|                                                                                  
    ;                                                                                                        
                                                                                                             
                                                                                                             
    data _null_;                                                                                             
     length method $6 digest $128;                                                                           
     do method='CRC32','MD5','SHA1','SHA256';                                                                
     digest = hashing(method,'99999');                                                                       
     put method ': ' digest;                                                                                 
     end;                                                                                                    
     run;                                                                                                    
    run;                                                                                                     
                                                                                                             
    CRC32  : F8C1A4BB                                                                                        
    MD5    : 36678968064D487BB169300312CBCF2B                                                                
    SHA1   : 589205D6D61D7C2F0C8D2F4B29D6DB9ACA3A91D7                                                        
    SHA256 : FEA2EA1F88FF2AB557A8EC16CB7C977886DC2A819430A9615038A9FA922806E3                                
                                                                                                             
                                                                                                             
