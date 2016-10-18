##SELECT

    SELECT * FROM #select data (* = all) from table
    
    SELECT DISTINCT # select unique values only
    
    SELECT TOP #specify number or % #specify number or % of records displayed
    
    AS # alias to rename column heading locally

##FILTER

    WHERE #filter
    
    AND/OR #used after WHERE operators: true/either conditions
    
    LIKE #used after WHERE to search for pattern 
    
    IN () #used after WHERE to specify multiple values
    
    BETWEEN #used after WHERE with AND to select values in range
    
    NOT #used after WHERE to select values excluded from condition
    
    IS NULL/ IS NOT NULL #select missing values/all non missing values
    
    = #equal
    <> #not equal

##FUNCTIONS
    
    AVG() #return average value
    
    COUNT() #return number of rows
    
    MAX() / MIN() # return largest/smallest value
    
    SUM() #return sum
    
    UCASE()/LCASE() #convert field to upper/lower case
    
    ROUND() #round numeris field to specified #of decimals 
    
    LEN() #return length of test field
    
     ORDER BY() #sort result by one or more columns

##TABLES    

    JOIN #combine tables: inner, left, right & full 
    
    UNION #combine results of 2 or more SELECTS
    
    SELECT INTO #copy info from one table into new other table
    
##CHARACTERS

    % #substitute for unknown characters
    
    _ #substitute for single character
    
    [charlist] #sets/ranges of characters to match 
    
    [^charlist] or [!charlist] #match only a character not specified within
