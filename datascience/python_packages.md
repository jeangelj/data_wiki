##numpy

    import numpy as np
    np.log
    arr = array([])
    arr.shape #shape of an array
    convolve(a,b) #linear convolution of two sequences
    dot(arr1,arr2) #compute inner product of two arrays
    vectorize() #turn scalar function into one accepting/returning vectors
    np.log(train_data['SalaryNormalized']).plot()

##pandas

    import pandas as pd
    df = pd.read_csv (“path/data.csv”) #returns dataframe
    df.head() #see top rows of dataframe
    len(df) #number of rows
    df.describe() #descriptive statistics
    df.info() #general info
    df.column.value_counts() #count of each value
    df.column.unique() #same as value counts
    df.column.nunique() # number of unique entries

    df[[‘column’]] #select/returns dataframe with column
    df[‘column’] #returns series; same as df.column
    df.iloc[label] #select row by label
    df.inbox #return dataframe index

    df.sort_values('column', ascending=False)
    new_df = df.merge(other_df, on='column') #columns must be in both dataframes
    concat() #merge dataframe or series objects
    df.drop()#delete row/column
    df.dropna() #drop rows where data is missing

    df.grouby() # split df by columns and create groupby object
    df.mean(); df.median(); df.std(); df.sort()
    df.min()/df.max() #return min/max of every column
    df.T() #transpose dataframe
    df.agg({‘column’:[mean,std]})
    pd.pivot_table(df, values=['column2', 'column4'], index=['column3'], columns=['column5']) #pivot table

    df [[‘column1’,’column2’,’column3’]][(df[‘column5’] >= 100) & (df[‘column2’]>10)].head() #where/and statement like SQL
    df[[‘column1’,’column2’,’column3’]].grouby(‘column2’).mean() #mean for each column grouped by column 2

    df.applymap() #apply function to every element in dataframe
    df.apply() #apply function along a given axis

    df.plot(x=’column1’,y=’column2’, kind=’scatter’)
    f = df.column.hist(bins = 20) #histogram df.hist(alpha =.5)
    pd.scatter_matrix(data, figsize=(10,10))

    df.to_csv(‘file.csv’) #save to csv
    read_csv(‘file.csv’) #read csv into dataframe
    df.to_excel(‘file.xlsx’, sheet_name) #save to excel
    read_excel(‘file.xlsx’,’sheet1’, index_col = None, na_values =[‘NA’]) #read excel into dataframe
    
    #add date index 
    year_salary.index = pd.to_datetime(year_salary.index, format="%Y") 

    #loop to display unique values with writing
    for col in test_data.columns: 
        print "%s has %s unique categories" % (col, test_data[col].nunique())
        
##matplotlib

    from matplotlib import pyplot as plt
    %matplotlib inline #% = in juptyer notebook, don't export graphic to file but display in line in notebook
    f = plt.plot(l)
    plt.plot(x, y, 'r:') #red dotted line; b-- #blue – line
    plt.title("title”), plt.xlabel("x-axis"), plt.ylabel("y-axis")
    plt.xlim(0, 5), plt.ylim(0, 70) #plot limits
    plt.plot(range(6), range(6), 'y*:', markersize=10, label="straight line")#* creates the star markers, s creates square ones
    f = plt.legend() #use f to suppress standard title
    plt.plot.kde #density

    f = plt.scatter(df.column1, df.column2, linewidth=0, alpha=.1)
    plt.subplot(n,x,y) #creates multiple plots; n- number of plots, x – number of horizontally displayed, y – vertically displayed
    xticks([],[]) #same for yticks; set tick values, first array for values, second for labels
    .plot(kind='barh') #horizontal bar plot

    savefig(‘image.png’) #save plot
    
    #horizontal bar plot
    df.plot(kind='barh') 

    #pie chart
    plt.pie(Contract_Time, labels=('permanent','contract'),startangle=80) 
    plt.axis('equal')
    plt.show()

    #overlaying histograms
    bins = np.linspace(1, 100000, 30)
    f = plt.hist(y, bins=bins)
    f = plt.hist(lasso_2.predict(X), bins=bins)

##vincent

    !pip install vincent
    import Vincent as v
    s = v.Bar(dataframe)
    s.axis_titles(x='Team', y='Salary')
    v.Scatter(year_salary)
    f = vincent.StackedBar(team_year_salary).legend(title='Teams')
    f.width, f.height = 800, 500
    
##seaborn

    !pip install seaborn
    import seaborn as sns
    sns.heatmap(data[data.columns[:10]]['column'], annot=True)
    sb.lmplot('column1','column2’, df) #create trendline
    f = sb.lmplot(x = 'yd', y='sl', data=data, ci=95)
    f = sb.lmplot(x = 'yr', y='sl', col='rk', row='sx', data=data)
    sb.boxplot (x=’column1’,y=’column2’,data)#similar violinplot
    sb.factorplot(x='yearID', y='HR', col='teamID', col_wrap=5, data=data)



