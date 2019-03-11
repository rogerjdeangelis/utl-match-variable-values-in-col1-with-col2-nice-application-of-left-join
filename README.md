# utl-match-variable-values-in-col1-with-col2-nice-application-of-left-join
Match variable values in col1 with col2 nice application of left join    
    Match variable values in col1 with col2 nice application of left join                                               
                                                                                                                        
    I assume ID1 is a primary key                                                                                       
                                                                                                                        
    github                                                                                                              
    https://tinyurl.com/y68nspxn                                                                                        
    https://github.com/rogerjdeangelis/utl-match-variable-values-in-col1-with-col2-nice-application-of-left-join        
                                                                                                                        
    Novinosrin                                                                                                          
    https://communities.sas.com/t5/user/viewprofilepage/user-id/138205                                                  
                                                                                                                        
    *_                   _                                                                                              
    (_)_ __  _ __  _   _| |_                                                                                            
    | | '_ \| '_ \| | | | __|                                                                                           
    | | | | | |_) | |_| | |_                                                                                            
    |_|_| |_| .__/ \__,_|\__|                                                                                           
            |_|                                                                                                         
    ;                                                                                                                   
                                                                                                                        
    data have;                                                                                                          
    input ID1 $ ID2 $ val;                                                                                              
    cards4;                                                                                                             
    A B 1                                                                                                               
    B A 2                                                                                                               
    C G 3                                                                                                               
    E . 4                                                                                                               
    F H 5                                                                                                               
    ;;;;                                                                                                                
    run;quit;                                                                                                           
                                                                                                                        
                                                                                                                        
    /*                                                                                                                  
     WORK.HAVE total obs=5                                                                                              
                                                                                                                        
       ID1    ID2    VAL                                                                                                
                                                                                                                        
        A      B      1                                                                                                 
        B      A      2                                                                                                 
        C      G      3                                                                                                 
        E             4                                                                                                 
        F      H      5                                                                                                 
    */                                                                                                                  
                                                                                                                        
    *            _               _                                                                                      
      ___  _   _| |_ _ __  _   _| |_                                                                                    
     / _ \| | | | __| '_ \| | | | __|                                                                                   
    | (_) | |_| | |_| |_) | |_| | |_                                                                                    
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                   
                    |_|                                                                                                 
    ;                                                                                                                   
                                                                                                                        
    WORK.WANT total obs=5     | RULES                                                                                   
                              |                                                                                         
    Obs  ID1    ID2    VAL    | FLAG                                                                                    
                              |                                                                                         
     1    A      B      1     |   1  ID1("A') is in column ID2(Row 2) so set fag to 1                                   
     2    B      A      2     |   1  ID1("B') is in column ID2(Row 1) so set fag to 1                                   
     3    C      G      3     |   0  "C" in not in any row of ID2                                                       
     4    E             4     |   0  "E" in not in any row of ID2                                                       
     5    F      H      5     |   0  "F" in not in any row of ID2                                                       
                                                                                                                        
    *          _       _   _                                                                                            
     ___  ___ | |_   _| |_(_) ___  _ __                                                                                 
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                               
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                               
                                                                                                                        
    ;                                                                                                                   
                                                                                                                        
    proc sql;                                                                                                           
       create                                                                                                           
           table want as                                                                                                
       select                                                                                                           
           a.*                                                                                                          
         ,(a.id1=b.id2) as Flag                                                                                         
       from                                                                                                             
           have a left join have b                                                                                      
       on                                                                                                               
           a.id1=b.id2;                                                                                                 
    quit;                                                                                                               
                                                                                                                        
                                                                                                                        
