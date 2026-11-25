# NoShowGuard-Capstone-Project-
https://github.com/anshulvaidya/NoShowGuard-Capstone-Project-

Task 1.2 Number of Duplicate rows 20 after cleaning ----------------------------------------
Row count after (a) dropping duplicates: 1000
Row count after (b) cleaning booking_channel: 1000
Row count after (c) converting dates: 1000
Row count after (d) dropping missing appt_date or status: 990 

Task 1.3 --
Values capped in distance_km: 26
Values capped in fee_inr: 3

Task 1.4--
Column means (age, distance_km, fee_inr, lead_days): [ 48.17373737   9.50090909 635.71414141  11.81919192]
Rows with lead_days > 14: 296 (Share: 0.2990)
Rows with |z| > 2 for distance_km: 53

Task 3.1--
Training set size: 792
Test set size: 198
Number of no-shows in test set: 49
Baseline accuracy (always predicting Attended): 0.7525 (75.25%)

Task 3.2--
--- Test Set Evaluation Metrics ---
Accuracy:  0.7879
Precision: 0.6296
Recall:    0.3469
F1 Score:  0.4474
ROC-AUC:   0.7889

Confusion Matrix:
[[139  10]
 [ 32  17]]

--- Feature Coefficients (Scaled) ---
                Feature  Coefficient
                    age    -0.253880
            distance_km     0.253448
                fee_inr     0.452761
              lead_days     0.614471
         prior_no_shows     0.649612
          reminder_sent    -0.580669
    booking_channel_App    -0.046804
  booking_channel_Phone     0.215881
booking_channel_Walk-In    -0.186364
visit_type_Consultation     0.015658
   visit_type_Follow-up    -0.015658

--- Odds Ratio for reminder_sent ---
Scaled np.exp(coef):              0.5595
Unscaled np.exp(coef / scale_):   0.3094

Task 3.3--
--- Decision Tree (No Depth Limit) ---
Training Accuracy: 1.0000
Test Accuracy:     0.6717
Gap (Train - Test): 0.3283

--- Decision Tree (max_depth=3) ---
Training Accuracy: 0.8220
Test Accuracy:     0.7778
Gap (Train - Test): 0.0442

Task 3.4 --
--- Random Forest Test Set Metrics ---
Accuracy: 0.7475
Recall:   0.3061
ROC-AUC:  0.7057

--- Top 3 Feature Importances ---
lead_days      0.219905
age            0.196788
distance_km    0.194739

--- Model Comparison Summary ---
                           Model  Accuracy  Recall  ROC-AUC
             Logistic Regression    0.7879  0.3469   0.7889
     Decision Tree (max_depth=3)    0.7778  0.2245   0.6997
Random Forest (n_estimators=100)    0.7475  0.3061   0.7057

Task 3.5--
--- (a) GridSearchCV Results ---
Best Params: {'max_depth': 3, 'n_estimators': 200}
Best CV ROC-AUC: 0.7673

--- (b) 5-Fold Cross-Validated ROC-AUC Comparison ---
Logistic Regression           : 0.7737
Decision Tree (max_depth=3)   : 0.6784
Random Forest (default)       : 0.7466
Random Forest (tuned)         : 0.7673

Winner Selected: Logistic Regression (CV ROC-AUC = 0.7737)

--- (c) Threshold Comparison on Training OOF Predictions ---
Threshold 0.50 -> Precision: 0.5753 | Recall: 0.2485 | F1: 0.3471 | Flagged: 73
Threshold 0.35 -> Precision: 0.5130 | Recall: 0.4675 | F1: 0.4892 | Flagged: 154

Chosen Threshold (higher F1): 0.35

--- (d) Final One-Time Evaluation on Test Set ---
Chosen Threshold: 0.35
Test Precision:   0.5714
Test Recall:      0.5714
Number Flagged:   49 (out of 198 test rows)
Test ROC-AUC:     0.7889

--- (e) Saved test_risk_scores.csv ---
    appointment_id  no_show  risk_prob  flag
213          A0217        0   0.021565     0
331          A0336        0   0.150917     0
501          A0508        0   0.518692     1
309          A0314        0   0.191300     0
88           A0089        0   0.167718     0

Task 4.3--
=== Error 1: confidence = 1.7 ===
1 validation error for FollowupInsight
confidence
  Input should be less than or equal to 1 [type=less_than_equal, input_value=1.7, input_type=float]
    For further information visit https://errors.pydantic.dev/2.14/v/less_than_equal

=== Error 2: missing recommended_action ===
1 validation error for FollowupInsight
recommended_action
  Field required [type=missing, input_value={'root_cause': 'transport...rrange a ride in time.'}, input_type=dict]
    For further information visit https://errors.pydantic.dev/2.14/v/missing

Task 4.1--
Enter your Gemini API Key: ··········
{'root_cause': 'forgot_or_no_reminder', 'confidence': 0.98, 'summary': 'Patient missed the appointment because she did not receive a reminder and forgot about it.', 'recommended_action': 'Reschedule the patient for next week and verify that automated SMS or call reminders are active.'}

Task 4.3 (a)--
=== Error 1: confidence = 1.7 ===
1 validation error for FollowupInsight
confidence
  Input should be less than or equal to 1 [type=less_than_equal, input_value=1.7, input_type=float]
    For further information visit https://errors.pydantic.dev/2.14/v/less_than_equal

=== Error 2: missing recommended_action ===
1 validation error for FollowupInsight
recommended_action
  Field required [type=missing, input_value={'root_cause': 'transport...rrange a ride in time.'}, input_type=dict]
For further information visit https://errors.pydantic.dev/2.14/v/missing

Task 4.3 (c)--
=== Task 4.3 (c): API Call Summary ===
Task 4.1 API calls: 1
Task 4.2 API calls: 9 (10 rows minus blank/skipped rows)
Task 4.3 API calls: 4 (2 notes x 2 prompts)
Total API calls across Tasks 4.1–4.3: 14

