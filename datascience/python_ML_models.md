##model

    ##Import model from sklearn
    X = data[features]  # put our features in a separate matrix, this is the 'input'
    y = data.species  # these are the labels to predict/ response
    from sklearn.cross_validation import train_test_split
    X_train, X_test, y_train, y_test = train_test_split(X, y, train_size=.7, random_state=42) #cross validation: 70% of data for training; random state 42 or 123
    model = model()
    model.fit(X_train, y_train)
    train_accuracy = model.score(X_train, y_train)
    test_accuracy = model.score(X_test, y_test)
    y_prediction  = model.predict(x_test)
    preds = pd.DataFrame(y_prediction, columns=['Salary'])
    preds.to_csv('/Users/username/Desktop/file.csv')

##cross validation

    ##from sklearn.cross_validation import KFold
    cv = KFold(len(data), n_folds=5, shuffle=True)
    #Provides train/test indices to split data in train test sets. Split dataset into k consecutive folds 

    cross_scores = []
    for k in xrange(1, 10):
        model = model()
        cross_score = cross_val_score(model, X, y, cv=5)
        cross_scores.append(cross_score.mean())
    plt.plot(cross_scores)

    #model performance
    for metric in ["accuracy", "precision", "recall", "f1", "roc_auc"]:
        print "%-10s: %.4f" % (metric, cross_val_score(model, X, y, cv=10, scoring=metric).mean())

    from sklearn.metrics import mean_absolute_error
    mean_absolute_error(data.y, data.y_pred)
    #MAE = np.mean(abs(data.y - data.y_pred))
    mean_squared_error(data.y, data.y_pred)
    #MSA = np.square(data.y_pred - data.y).mean()

    print -cross_val_score(lasso_2, X, y, cv=10, scoring="mean_absolute_error").mean()
    print -np.median(cross_val_score(lasso_2, X, y, cv=10, scoring="median_absolute_error"))

    #compare models
    models = [(‘RFC’, RandomForestClassifier(n_estimators=200))
        ,(‘GBC’,GradientBoostingClassifier(n_estimators=100))
        ,(‘DTC’,DecisionTreeClassifier())
        ,(‘ABC’,AdaBoostClassifier())]
    results = {}
    for model, clf in models:
        score = cross_val_score(clf, X2, Y_target).mean()
        results[model] = score
        
##Reguralization 

    from sklearn.linear_model import Ridge, Lasso, RidgeCV
    from sklearn.preprocessing import PolynomialFeatures, StandardScaler
    from sklearn.pipeline import make_pipeline

    lasso_model = Lasso(alpha=.01) # imposes L1 prior on coefficient (→ many coeffiecients become zero); the higher the alphoa the more you penalize coefficients
    ridge_model = Ridge(alpha = 2.0)
    #Ridge regression imposes L2 prior on coefficient → outliers to be less likely and coeffiecients to be small across the board
    ridgeCV_model = RidgeCV  (alphas=[0.1, 1.0, 10.0]) #several alphas at once for comparison

    model = make_pipeline(StandardScaler(), PolynomialFeatures(degree), test_model)
    make_pipeline # chain multiple estimators into one
    PolynomialFeatures(degree)#Generate a new feature matrix consisting of all polynomial combinations of the features with specified degree
    StandardScaler()#Standardize features by removing the mean and scaling to unit variance
    
##Categorical Features

    from patsy import dmatrices # patsy provides R formula syntax
    y, X = dmatrices('y ~ column1 + column2 + column3', data=df, return_type='dataframe') #add columns for each category 0/1

    + #is not addition operator but separator between variables
    : #adds the interaction of two variables.
    * #adds the original terms as well as their interaction effect
    C() #make categorical

##Text Features – converting text to vectors

    from sklearn.feature_extraction.text import CountVectorizer, TfidfVectorizer, DictVectorizer

    #most used words
    words = pd.Series([word for line in data.column.values for word in line.lower().split()]).value_counts()
    words.head(20)

    #how many times a word is included
    data['word'] = data.column.map(lambda x: x.find('word') > -1)
    data.great.value_counts()

    #specify stopwords
    additional_stop_words = [‘word’,’word’]
    my_stop_words = text.ENGLISH_STOP_WORDS.union(additional_stop_words)

    cv = CountVectorizer(stop_words = my_stop_words, ngram_range=(1,2), max_features=5, min_df=.10, max_df=.95)
    #only use what appears at least some times, but not too often
    #class transforms an array-like (list, dataframe column, array) of strings into a matrix where each column represents a token (word or phrase) and each row represents the sample

    tv = TfidfVectorizer(stop_words = my_stop_words, ngram_range=(1,2), max_features=5, min_df=.10, max_df=.95)
    #Term Frequency is simply the number of times that a word appear in a sample

    X, y = cv.fit_transform(data.text).todense(), data.score

    #for each line see what words are present true/false
    pd.concat([pd.DataFrame(X, columns=cv.get_feature_names()), data.text], axis=1).head()

     #for model check which words are positive vs. negative
    coef = pd.Series(model.coef_, index=cv.get_feature_names())
    coef.sort()
    top = 15
    fig, axes = plt.subplots(1, 2, figsize=(12, 4))
    f = coef[:top].plot(kind='barh', ax=axes[0])
    f = coef[-top:].plot(kind='barh', ax=axes[1])
    print "Negative:", ", ".join(coef[:top].index)
    print "Positive:", ", ".join(coef[-top:].index)

    #
    dv = DictVectorizer(sparse=False)

##statsmodels

    import statsmodels.formula.api as sm
    # investigating results of a model & integrates with patsy
    model = sm.ols(formula="y ~ column1+ column2", data=df).fit()
    model.summary()

