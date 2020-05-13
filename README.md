# utl-embed-sql-code-inside-proc-report-using-dosubl
    Embed sql code inside proc report using dosubl                                                                                 
                                                                                                                                   
      Two Solutions                                                                                                                
                                                                                                                                   
          a. where dosubl                                                                                                          
          b. run time dosubl                                                                                                       
             Regards,                                                                                                              
             Richard DeVenezia                                                                                                     
                                                                                                                                   
          Interesting solution by Richard                                                                                          
                                                                                                                                   
             Richard embeds the dosubl inside a compute block.                                                                     
             The 'SQL' compute block is excecuted before the report is created but at run report time                              
             Also nice use of call execute, very useful for debugging?                                                             
                                                                                                                                   
    github                                                                                                                         
    https://tinyurl.com/y8jo6osj                                                                                                   
    https://github.com/rogerjdeangelis/utl-embed-sql-code-inside-proc-report-using-dosubl                                          
                                                                                                                                   
    sas forum                                                                                                                      
    https://tinyurl.com/y9gduwp3                                                                                                   
    https://communities.sas.com/t5/ODS-and-Base-Reporting/PROC-REPORT-compare-to-value-in-first-row/m-p/646189                     
                                                                                                                                   
    *_                   _                                                                                                         
    (_)_ __  _ __  _   _| |_                                                                                                       
    | | '_ \| '_ \| | | | __|                                                                                                      
    | | | | | |_) | |_| | |_                                                                                                       
    |_|_| |_| .__/ \__,_|\__|                                                                                                      
            |_|                                                                                                                    
    ;                                                                                                                              
                                                                                                                                   
     sashelp.class                                                                                                                 
                                                                                                                                   
                                                                                                                                   
    SASHELP.CLASS total obs=19                                                                                                     
                                                                                                                                   
      NAME       SEX    AGE    HEIGHT    WEIGHT                                                                                    
                                                                                                                                   
      Joyce       F      11     51.3       50.5                                                                                    
      Louise      F      12     56.3       77.0                                                                                    
      Alice       F      13     56.5       84.0                                                                                    
      James       M      12     57.3       83.0                                                                                    
      Thomas      M      11     57.5       85.0                                                                                    
    ....                                                                                                                           
                                                                                                                                   
    RULES                                                                                                                          
                                                                                                                                   
      Color all weights blue less than the average weight                                                                          
      Color all heights blue grester than the average height yellow                                                                
                                                                                                                                   
    *            _               _                                                                                                 
      ___  _   _| |_ _ __  _   _| |_                                                                                               
     / _ \| | | | __| '_ \| | | | __|                                                                                              
    | (_) | |_| | |_| |_) | |_| | |_                                                                                               
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                              
                    |_|                                                                                                            
    ;                                                                                                                              
                                                                                                                                   
    ----------------------------------------------                                                                                 
    |     Mean Height and Weight are 62 & 100    |                                                                                 
    |                                            |                                                                                 
    |NAME     SEX     AGE     HEIGHT     WEIGHT  |                                                                                 
    |--------------------------------------------|                                                                                 
    |Joyce   | F|      11|        51.3|BLUE  50.5|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |Louise  | F|      12|        56.3|BLUE    77|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |Alice   | F|      13|        56.5|BLUE    84|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |James   | M|      12|        57.3|BLUE    83|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |Thomas  | M|      11|        57.5|BLUE    85|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |John    | M|      12|          59|BLUE  99.5|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |Jane    | F|      12|        59.8|BLUE  84.5|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |Janet   | F|      15| YELLOW 62.5|     112.5|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |Jeffrey | M|      13| YELLOW 62.5|BLUE    84|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |Carol   | F|      14| YELLOW 62.8|     102.5|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |Henry   | M|      14| YELLOW 63.5|     102.5|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |Judy    | F|      14| YELLOW 64.3|BLUE    90|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |Robert  | M|      12| YELLOW 64.8|       128|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |Barbara | F|      13| YELLOW 65.3|BLUE    98|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |Mary    | F|      15| YELLOW 66.5|       112|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |William | M|      15| YELLOW 66.5|       112|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |Ronald  | M|      15| YELLOW   67|       133|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |Alfred  | M|      14| YELLOW   69|     112.5|                                                                                 
    |--------+--+--------+------------+----------|                                                                                 
    |Philip  | M|      16| YELLOW   72|       150|                                                                                 
    ----------------------------------------------                                                                                 
                                                                                                                                   
    *                                                                                                                              
     _ __  _ __ ___   ___ ___  ___ ___                                                                                             
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                                            
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                            
    | .__/|_|  \___/ \___\___||___/___/                                                                                            
    |_|                 _                          _                 _     _                                                       
      __ _    __      _| |__   ___ _ __ ___     __| | ___  ___ _   _| |__ | |                                                      
     / _` |   \ \ /\ / / '_ \ / _ \ '__/ _ \   / _` |/ _ \/ __| | | | '_ \| |                                                      
    | (_| |_   \ V  V /| | | |  __/ | |  __/  | (_| | (_) \__ \ |_| | |_) | |                                                      
     \__,_(_)   \_/\_/ |_| |_|\___|_|  \___|   \__,_|\___/|___/\__,_|_.__/|_|                                                      
    ;                                                                                                                              
                                                                                                                                   
    * just in case;                                                                                                                
    %symdel holdavg_h holdavg_w;                                                                                                   
    %utlfkil(d:/xls/dosubl_report.xlsx);                                                                                           
                                                                                                                                   
    ods excel file='d:/xls/dosubl_report.xlsx' options(sheet_name="class");                                                        
                                                                                                                                   
    proc report data=sashelp.class(                                                                                                
           where=(0=%sysfunc(dosubl('                                                                                              
              proc sql noprint;                                                                                                    
                select                                                                                                             
                   mean(height)                                                                                                    
                  ,mean(weight)                                                                                                    
                into                                                                                                               
                  :holdavg_h                                                                                                       
                 ,:holdavg_w                                                                                                       
                from                                                                                                               
                  sashelp.class                                                                                                    
              ;quit;                                                                                                               
             ')))                                                                                                                  
           );                                                                                                                      
        columns ( "Average Height and Weight are &holdavg_h and &holdavg_w repectively"                                            
          name sex age height weight);                                                                                             
                                                                                                                                   
          define name / display missing;                                                                                           
          define sex / display missing;                                                                                            
          define age / display missing;                                                                                            
          define height/display format=5.1;                                                                                        
          define weight/display format=5.1;                                                                                        
                                                                                                                                   
          compute weight;                                                                                                          
              if height gt &holdavg_h then                                                                                         
                 call define('height','style','style={background=yellow}');                                                        
                                                                                                                                   
              if weight lt &holdavg_w then                                                                                         
                 call define(_col_,'style','style={background=lightblue}');                                                        
          endcomp;                                                                                                                 
    run;quit;                                                                                                                      
    ods excel close;                                                                                                               
                                                                                                                                   
    *_                                        _             _                 _     _                                              
    | |__      ___ ___  _ __ ___  _ __  _   _| |_ ___    __| | ___  ___ _   _| |__ | |                                             
    | '_ \    / __/ _ \| '_ ` _ \| '_ \| | | | __/ _ \  / _` |/ _ \/ __| | | | '_ \| |                                             
    | |_) |  | (_| (_) | | | | | | |_) | |_| | ||  __/ | (_| | (_) \__ \ |_| | |_) | |                                             
    |_.__(_)  \___\___/|_| |_| |_| .__/ \__,_|\__\___|  \__,_|\___/|___/\__,_|_.__/|_|                                             
    ;                            |_|                                                                                               
                                                                                                                                   
    Example:                                                                                                                       
    Still a bit Mickey Mouse,                                                                                                      
    but suppose the report was coloring based on like-sexed average height and weight.                                             
                                                                                                                                   
    %symdel H_MEAN_M W_MEAN_M H_MEAN_F W_MEAN_F /nowarn;                                                                           
                                                                                                                                   
    %symdel holdavg_h holdavg_w;                                                                                                   
    %utlfkil(d:/xls/dosubl_report.xlsx);                                                                                           
                                                                                                                                   
    ods excel file='d:/xls/dosubl_report.xlsx' options(sheet_name="class");                                                        
                                                                                                                                   
    proc report data=sashelp.class;                                                                                                
        columns name sex age height weight;                                                                                        
                                                                                                                                   
          define name / display missing;                                                                                           
          define sex / display missing;                                                                                            
          define age / display missing;                                                                                            
          define height/display format=5.1;                                                                                        
          define weight/display format=5.1;                                                                                        
                                                                                                                                   
          compute weight;                                                                                                          
            *******************************************************;                                                               
            * dynamic code gen and execution during Proc run-time *;                                                               
            *******************************************************;                                                               
            if not symexist ('H_MEAN_'||sex) then rc = doSubl('                                                                    
              proc sql noprint;                                                                                                    
                select mean(height) format=rb8., mean(weight) format=rb8.                                                          
                into      :H_MEAN_'||sex||',    :W_MEAN_'||sex||'                                                                  
                from sashelp.class                                                                                                 
                where sex = "'||sex||'";                                                                                           
            ');                                                                                                                    
                                                                                                                                   
            h_mean = input(symget("H_MEAN_"||sex),rb8.);                                                                           
            w_mean = input(symget("W_MEAN_"||sex),rb8.);                                                                           
                                                                                                                                   
            call execute ('%put sex='||sex||' h_mean='||h_mean||' w_mean='||w_mean);                                               
                                                                                                                                   
            h_color = ifc(sex='F','yellow', 'CXAAAA00');                                                                           
            w_color = ifc(sex='F','lightblue', 'VLIGB');                                                                           
                                                                                                                                   
            if height gt h_mean then                                                                                               
                 call define('height','style','style={background='||h_color||'}');                                                 
                                                                                                                                   
            if weight lt w_mean then                                                                                               
                 call define('weight','style','style={background='||w_color||'}');                                                 
          endcomp;                                                                                                                 
    run;quit;                                                                                                                      
                                                                                                                                   
    ods excel close;                                                                                                               
                                                                                                                                   
                                                                                                                                   
Regards,                                                                                                                           
Richard DeVenezia                                                                                                                  
                                                                                                                                   
