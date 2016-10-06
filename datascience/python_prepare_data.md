kaggle data titanic example 
https://www.kaggle.com/c/titanic

##clean data

    #clean up Sex into boolean 0 and 1 
    train_data['Sex'] = train_data['Sex'].map( {'female': 0, 'male': 1} ).astype(int)

    # All the missing Fares -> assume median of their respective class
    if len(train_data.Fare[train_data.Fare.isnull() ]) > 0:
        median_fare = np.zeros(3)
        for f in range(0,3):                                              # loop 0 to 2
            median_fare[f] = train_data[train_data.Pclass == f+1 ]['Fare'].dropna().median()
        for f in range(0,3):                                              # loop 0 to 2
            train_data.loc[ (train_data.Fare.isnull()) & (train_data.Pclass == f+1 ), 'Fare'] = median_fare[f]

    # All missing Embarked -> just make them embark from most common place
    if len(train_data.Embarked[ train_data.Embarked.isnull() ]) > 0:
        train_data.Embarked[ train_data.Embarked.isnull() ] = train_data.Embarked.dropna().mode().values
    Ports = list(enumerate(np.unique(train_data['Embarked'])))
    Ports_dict = { name : i for i, name in Ports }
    train_data.Embarked = train_data.Embarked.map( lambda x: Ports_dict[x]).astype(int)

    # All the ages with no data -> make the median of all Ages
    median_age = train_data['Age'].dropna().median()
    if len(train_data.Age[ train_data.Age.isnull() ]) > 0:
        train_data.loc[ (train_data.Age.isnull()), 'Age'] = median_age

    #substitute all NaN with 0 
    train_data = train_data.fillna(0)

    # substitute all cabin numbers to 1, in other words we transformed this column into saying, if the person had a cabin or not
    train_data.loc[train_data['Cabin'] > 0, 'Cabin'] = 1

##add columns/features

    #add column "married woman", if brackets in name
    train_data['married woman'] = train_data.Name.map(lambda x: int(str(x).lower().find('(') > -1) if x is not None else None)

    #add dependents column - if you were alone on the boat = 0 
    train_data['dependents'] = train_data.SibSp + train_data.Parch

    #want to establish their richness level 
    train_data['richness'] = train_data.Fare/train_data.Pclass

    #add log column of column
    richness2 = np.log(np.sqrt(train_data[['richness']]))

    #add log square root column
    age2 = np.log(np.sqrt(train_data[['Age']]))
