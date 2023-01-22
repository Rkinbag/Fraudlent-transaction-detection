# Fraudlent-transaction-detection
## Q&A
# QUESTIONS TO ANSWER

* Data cleaning including missing values, outliers and multi-collinearity.
* Describe your fraud detection model in elaboration.
* How did you select variables to be included in the model?
* Demonstrate the performance of the model by using best set of tools.
* What are the key factors that predict fraudulent customer?
* Do these factors make sense? If yes, How? If not, How not?
* What kind of prevention should be adopted while company update its infrastructure?
* Assuming these actions have been implemented, how would you determine if they work?

## ANSWERS

* Dataset contains no missing values, but after feature engineering vif of few features was very high so I use VIF to remove them.
This will answered by combining all of answers of this question will be answered by following answers.
* I bascially dropped thew columns which doesnt provide any information gain and have very high VIF ( variance influence factor), apart from that I performed feature    engineering and lastly took all the columns which got left.
* I have provided various metrics, as accuracy is not a good metric for imbalanced dataset , I have provide classification reports which provide precision,recall anf F1 score(recommended for imbalanced dataset).
* I have performed the process of feature importance by using mututal information,Mutual Information measures the entropy drops under the condition of the target value. by that I found the most imortant fearures are following in decreasing importance or information gain:
  * type
  * possible_fraud2
  * origin_bal_change
  * possible_fraud
  * amount
  * isFlaggedFraud
* Type: I performed feature engineering on feature TYPE, what I found was that the proproptions of fraud transactions when looked in terms of unique values in column type (which is basically column for transaction type) is only given by two types of transaction CASH_OUT (50.11567) TRANSFER (49.88433), what that means is all fraud transactions are either cash_out or transfer of amount to different account which makes sense as fraud transaction will be done either taking fraud money out from someone's account or transferring it to diffferent account. I mapped 1 to both cash_out and transfer and 0 to other values , so basically I weighted them and give more preference for genuine reason.

* origin_bal_change: In fraudulent transactions, the origin account is completely emptied out (almost), so this feature provides a unique perspective about fraudlent transactions and its also be seen by the kernel density plot for newbalanceorigin. it also makes sense as no one empty their account during any transaction, empyting account can lead to expiration of the account itself, so it clearly implies their is fraudlent transaction.

* possible_fraud: this feature again was made during feature engineering, this feature bascially consider those transaction which involve emptying the originaccount balance as we have seen that in fraudlent transaction this is prominent so I have marked 1 all such transcations.

* possible_fraud2: this feature takes account the fact that in fraudulent transactions, the newbalance in the destination account does not increase at all, the change is 0 , I have marked all those transaction as 1 which are not previosly marked as 1 by possible fraud feature and isFlaggedFraud so that we can gain new information and multicollinearaity remain distant. This can be seen by KDE Plot clearly.

* amount: In KDE Plot for amount we can see that when transaction amount increases the number of fraudlent transaction also increases, not only that at bveyond certain amounts (2x10^^) the fraudlent transaction are significantly higher than non fraud transactions which makes sense as fraudlentr transction usally involve large sums of money.

* The rest features have no strong reason for their relationships

* The company should contact the account holder as soon as the transaction amount crosses 30% of their balance in account and should not let them totally empty their account, by that they can significantly decrease fraudlent transaction.
To check the efficiency of step above take, they can first all check the number of fraudlent transaction further they can run a model like this and check the feature importance, if the feature importance of features which were considered during decision making decreasing that means that feature did its work and rest fraudlent transactoin have no significant relationship with that feature and futher they can check other features and take steps accordinly.
