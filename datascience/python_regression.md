


##R-squared and adjusted r-squared

from sklearn.linear_model import LinearRegression
model = LinearRegression()
X, y = df[['NumberofEmployees','ValueofContract']], df.AverageNumberofTickets
model.fit(X, y)

###compute with formulas from the theory
yhat = model.predict(X)
SS_Residual = sum((y-yhat)**2)
SS_Total = sum((y-np.mean(y))**2)
r_squared = 1 - (float(SS_Residual))/SS_Total
adjusted_r_squared = 1 - (1-r_squared)*(len(y)-1)/(len(y)-X.shape[1]-1)
print r_squared, adjusted_r_squared
> 0.877643371323 0.863248473832

###compute with sklearn linear_model, although could not find any function to compute adjusted-r-square directly from documentation
print model.score(X, y), 1 - (1-model.score(X, y))*(len(y)-1)/(len(y)-X.shape[1]-1)
> 0.877643371323 0.863248473832 

###compute with statsmodels, by adding intercept manually
import statsmodels.api as sm
X1 = sm.add_constant(X)
result = sm.OLS(y, X1).fit()
print dir(result)
print result.rsquared, result.rsquared_adj
> 0.877643371323 0.863248473832

###compute with statsmodels, another way, using formula
import statsmodels.formula.api as sm
result = sm.ols(formula="AverageNumberofTickets ~ NumberofEmployees + ValueofContract", data=df).fit()
print result.summary()
print result.rsquared, result.rsquared_adj
> 0.877643371323 0.863248473832
