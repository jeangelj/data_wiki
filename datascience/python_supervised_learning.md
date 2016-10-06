##knn (k nearest neighbors algorithm): 
Euclidean distance, can be used for both classification and regression; instance based learning; lazy learning; might need to rescale data to make dimensions comparable

    from sklearn.neighbors import KNeighborsClassifier 
    model = KNeighborsClassifier(n_neighbors=5)

    loop to go through different n_neighbors options:
    scores = []
    for k in xrange(1,100):
        model = KNeighborsClassifier(n_neighbors=k)
        model.fit(X_train, y_train)
        score = model.score(X_test, y_test)
        scores.append(score)
    plt.plot(scores)

##logistic regression

    dependent variable is categorical

    from sklearn.linear_model import LogisticRegression

    decision boundary:
    x1, x2 = features
    colors = list("rby")

    # Plot the flowers with color labels
    for spec in data.species.unique():
        data_spec = data[data.species == spec]
        plt.scatter(data_spec[x1], data_spec[x2], label=spec, c=colors.pop(),
                    linewidths=0, s=100, alpha=.4)

    # draw the decision boundary
    boundary_x1 = np.array([data[x1].min() - .3, data[x1].max() + .3])
    boundary_x2 = -(model.intercept_ + model.coef_[0, 0] * boundary_x1) / model.coef_[0, 1]
    f = plt.plot(boundary_x1, boundary_x2, ':')
    f = plt.legend(loc="upper left", bbox_to_anchor=(1,1))
    f = plt.xlabel(x1), plt.ylabel(x2)
    
##Naïve Bayes

P(A|B) = (P(B|A)*P(A))/P(B)  (you can swap conditional probabilities); can be easily updated in real time; optimize either P(A|B) or P(A|B)P(A) - update our beliefs based on new evidence; MLE (maximum likelihood estimator) finds the parameters that make the data most likely 

    from sklearn.naive_bayes import GaussianNB
    from sklearn.naive_bayes import MultinomialNB

##Decision Tree – Random Forest

non-parametric hierarchical; nodes represent questions (“test conditions”) and edges are answers to these questions (edges lead from parent node to child node starting from root node and ending in leaf nodes = class labels) → binary yes/no answers; gild (grow) a decision tree = Hunt’s algorithm (greedy recursive algorithm →goal highest possible purity: Entropy (information gain) coefficient, Gini coefficient, Misclassification Error)

    from sklearn.tree import DecisionTreeClassifier
    from sklearn.ensemble import RandomForestClassifier
    model = DecisionTreeClassifier (criterion =’gini’) # single tree #here you can change the algorithm as entropy or gini
    model = RandomForestClassifier(n_estimators=20, n_jobs=6) 

    #important features
    model.feature_importances_ 
    from sklearn.ensemble import ExtraTreesClassifier
    etc_model = ExtraTreesClassifier()
    etc_model.fit(X, Y_target)
    df = pd.DataFrame(etc_model.feature_importances_, index = X.columns.values, columns =['importance'])

    #optimize model
    %time
    scores = []
    for n in [1, 2, 3, 5, 10, 20, 50, 100, 200, 300]:
        for criterion in ['gini', 'entropy']:
            start_time = time.time()  # let's time it, to see how long running a forest takes
            r_model = RandomForestClassifier(n_estimators=n, criterion=criterion)
            accuracy = cross_val_score(r_model, X, Y_target).mean()  # out of sample accuracy
            duration = time.time() - start_time
            scores.append(dict(n_estimators=n, criterion=criterion, accuracy=accuracy, duration=duration))
    scores = pd.DataFrame(scores)

##SVM (Support Vector Machine)

decision boundary that makes the most sense based on analytic geometry; generalization error = margin (area around line without points) → margin depends only on subset of training data nearest to line → create line with largest margin (maximum margin hyperplane) → convex objective function - take derivative and equal to zero to find max

    from sklearn import svm
    model = svm.SVC() #create SVM classification object
    
##boosting

Boosting (convert weak learners to strong learners) - classifier for classification and regressor for regression
Ada Boost; Gradient Boosting; XGBoost

    From sklearn.ensemble import GradientBoostingClassifier, AdaBoostClassifier

    model = AdaBoostClassifier(n_estimators=10)
    %time cross_val_score(model, X, data.target).mean()

    X_array = X.toarray()  # Covert to dense matrix (model won't accept sparse matrices)
    model = GradientBoostingClassifier(n_estimators=k)

