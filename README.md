# Problem Set 5: Right 93% of the Time
ECON 3916 · Module 3: The ML Pipeline · Yushan Li
**To:** Head of Risk  
**Re:** Default model sign-off

**Recommendation: sign, on two conditions:** deploy the model with a 14.5% decline threshold, not 50%, and confirm its calibration on a fresh cohort of applications first.

The vendor's 93% proves nothing. On our test set, approving every applicant scores 93.2%. The penalised logistic model reaches 95.1%, under two points better than doing nothing. Its real value is in dollars. On 3,000 test applications, approving everyone loses $2.42M; the model at the standard 50% threshold loses $1.67M; at the cost-optimal threshold it loses $1.06M, 56% less than approving everyone.

The threshold comes from costs, not statistics. A missed default costs 60% of principal; declining a good applicant costs 8% in lost margin plus 2% for reputation, 10% in total. Decline whenever the predicted default probability exceeds 10 / (10 + 60), about 14%. If either cost changes, recompute with the same formula. At 14.5% we catch 76% of defaulters instead of 35%, at the price of declining 234 good applicants instead of 16.

Use the logistic model, not the random forest. The forest is no better (McNemar p = 0.47), and the logistic model can be explained to a regulator.

**What would change my answer:** the threshold works only because the model's probabilities are calibrated; when it predicts 20%, about 19% default. If a fresh cohort showed predicted and actual default rates drifting apart, the 14% rule would misfire, and I would recalibrate before using it.
