# AML_hack

As a team representing NuLuamPremiu, comprised of Alex Deonise, Bogdan Grecu, Razvan Mihaescu, and Daria Ciobanu, we present our solution to the BT-AML challenge.

Firstly, let's delve into the data preprocessing steps we employed. We utilized one-hot encoding for various categorical features such as From Bank, Account, To Bank, Account.1, Payment Currency, Receiving Currency, and Payment Format. To maintain the sequential nature of transactions, we normalized the Timestamp. While we experimented with alternative methods, such as merging From Bank and Account features, and To Bank and Account.1 features, we found that reducing the number of parameters negatively impacted the performance of our autoencoder model. We also explored converting all currencies to US Dollar but decided against it due to potential loss of information.

Our approach centers around training an autoencoder solely on legitimate transactions, with the hypothesis that the reconstruction loss of legitimate transactions would be notably lower than that of transactions involved in money laundering. We drew inspiration from Variational Autoencoders and Wasserstein Generative Adversarial Networks for Improving the Anti-Money Laundering Process[1].

Our autoencoder model consists of 10 neurons in the input layer corresponding to the 10 features used. We then have progressively narrower layers (8, 6, and 5 neurons) representing the encoder, with symmetric layers for the decoder. The loss function used is the reconstruction loss.

Following training on the fair transactions dataset which was made on the  HI-Small_Trans.csv[2], we evaluated the model's performance on the provided datasets. We implemented the data preprocessing pipeline within the evaluation process, calculating reconstruction errors to determine the authenticity of transactions. Transactions with errors above a certain threshold were flagged as fraudulent.

The threshold selection can be optimized using the ROC curve, aiming for the point closest to the top-left corner. The prediction time was approximately 4 seconds on the small dataset and 380 seconds on the large dataset.

Regarding adapting the model to data from a single bank with more client-specific information but lacking the overview of money flow, the adaptation process would be straightforward. With more features available, we can select only the most relevant ones, potentially discarding less informative features like currency. This adaptation would involve adjusting the number of neurons in the input and output layers, as well as potentially modifying the intermediate layers.

We also considered implementing a graph neural network. However, from our review of "Provably Powerful Graph Neural Networks for Directed Multigraphs"[3], we found that the model's performance was heavily dependent on complexity, which we couldn't implement due to time constraints. Furthermore, such a model wouldn't be suitable for a single-bank dataset since the edges in graph neural networks[4] connect accounts where money is transferred, and accounts in other banks wouldn't have corresponding nodes. Additionally, edge connections in a graph neural network would require nodes that might not exist in a single-bank dataset.


For metrics, we tested on two datasets:

1. ### Small_AML_ChallangeHB2.csv

* prediction time is: 4s
* accuracy = 0.974
* precison = 0.006
* recal = (0.140
* f1_score = 0.011
* AUC = 0.405
* ROC Curve: ![image](https://github.com/Maxxtra/AML-Detection-System/assets/83414814/e12ef937-68f9-4cd3-9b83-d6fe3ac585a6)

* Confusion Matrix: ![image](https://github.com/Maxxtra/AML-Detection-System/assets/83414814/5a2fb7af-b491-478e-a04a-3fc87dde40f7)

2. ## AML_ChallangeHB2.csv
   
* prediction time: 380s
* acc = 0.873
* prec = 0.005
* recal = 0.230
* f1 = 0.009
* AUC = 0.444
* ROC Curve: ![image](https://github.com/Maxxtra/AML-Detection-System/assets/83414814/9070efbf-a6b1-4bd1-b803-460cf47565c9)

* Confusion Matrix: ![image](https://github.com/Maxxtra/AML-Detection-System/assets/83414814/8a4e6fb9-4650-468c-a183-db4c62efc27e)


Bibliography:

[1] Variational Autoencoders and Wasserstein Generative Adversarial Networks for Improving the Anti-Money Laundering Process: ZhiYuan Chen1,ZhiYuan Chen1, Member, IEEE, Waleed Soliman1, Amril Nazir2, and Mohammad Shorfuzzaman3, Member, IEEE: https://www.researchgate.net/publication/352142543_Variational_Autoencoders_and_Wasserstein_Generative_Adversarial_Networks_for_Improving_the_Anti-Money_Laundering_Process

[2] IBM Transactions for Anti Money Laundering (AML): https://www.kaggle.com/datasets/ealtman2019/ibm-transactions-for-anti-money-laundering-aml

[3] Provably Powerful Graph Neural Networks for Directed Multigraphs: Béni Egressy, Luc von Niederhäusern, Jovan Blanuša, Erik Altman, Roger Wattenhofer, Kubilay Atasu2: https://arxiv.org/pdf/2306.11586.pdf

[4] Multi-GNN: https://github.com/IBM/Multi-GNN/blob/main/models.py
