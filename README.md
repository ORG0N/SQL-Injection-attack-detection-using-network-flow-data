# SQL-Injection-attack-detection-using-network-flow-data

This project aims to detect SQL Injection Attack (SQLIA's) using network flow data collected from relational database engines such as MySql,PostgreSQL and SQL Server; apply the data to ML models to determine the better accuracy with minimal execution time.

Overview:
* Basically SQLIA stands for sql Injection Attack where malicious SQL statements are inserted into 
  an user input field/Entry field for Execution, Allowing the System to comprise and bypass the 
  application security, manipulate databases and performing unauthorized operations.

Data Collection:
 * Source: NetFlow Version 5, a protcol developed by Cisco for collection IP Traffic data
 * Containing source and destination IP's,packet and byte counts, timestamp and so on.
   
Methology:
(i) Feature Cleaning:

     * First, the IP addresses were converted into numeric value, and 
     * dataset are checked for empty columns/rows to avoid error in generation of models.Rows with NA and infinity values are replaced with global constants/removed.
     * Dimensionality Reduction: purpose to reduce the complexity of model which increase by exponential times.
     * The process involues computing the variance of features and eliminated by mini,zero variance.
     * The features "exadrr","engine_type", 'src_mask', 'dst_mask', 'src_ac', and 'dst_as' were eliminated due to their variance being computed as 0 indicating no variation across             malicious and benign flows
     * Additionally, "unix_secs", 'unix_nsecs', 'sysuptime', 'first', and 'last' were removed to mitigate bias in the models introduced by temporal factors.
     * Finally, the 'nexthop' feature was excluded from the dataset due to its negative impact on the detection of malicious traffic in wide area networks.

(ii) Data Normalization:           
                    
          * Ensuring all features contribute equally to the model performance by scaling them to standard range.
          * Method: Applied Min-Max,Robust Scaling Normalization

(iii) Algorithm Implementation:

            * Algorithm: KNN, logistic Regression(LR),linear SVC, Perceptron with SGD and                     Random Forest(RF), Ensembled Technique(Voting Classifier)
            * Model Training: Partitioned Dataset into 80% for training and 20% for testing,                  Evaluated based on Accuracy of the model as well as with Minimal Execution time.
