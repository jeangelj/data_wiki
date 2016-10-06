    import sqlite3
    conn= sqlite3.connect('mxm_dataset.db') #connect to database
    c = conn.cursor() # from that connection, get a cursor to do queries

    #list tables in database
    q = "SELECT name FROM sqlite_master WHERE type='table' ORDER BY name" 
    res = c.execute(q) 
    print res.fetchall()

    conn.close() #close the connection

    # list column names
    q = "SELECT sql FROM sqlite_master WHERE tbl_name = 'songs' AND type = 'table'" 
    res = c.execute(q) 
    print res.fetchall()[0][0]

##write sqlite database as csv:

    import pandas.io.sql as sql
    table = sql.read_sql('select * from some_table', con) table.to_csv('output.csv')
