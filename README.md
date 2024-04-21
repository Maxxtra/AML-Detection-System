# AML_hack

1. Se încarcă un model autoencoder pre-antrenat dintr-un fișier salvat.
2. Se face o predicție folosind autoencoderul pentru datele de antrenare (X_train) pentru a obține o reconstrucție.
3. Se calculează eroarea de reconstrucție (mean squared error - MSE) între datele de intrare și predicțiile autoencoderului.
4. Se creează un DataFrame (error_df) care conține MSE și etichetele de clasă reale.
5. Se definesc niște praguri de eroare (thresholds) pentru a clasifica datele ca fiind normale sau anormale.
6. Se grupează datele după clasa reală (Minor sau Normal).
7. Se afișează un grafic care arată eroarea de reconstrucție pentru fiecare punct de date, iar pragurile sunt marcate cu linii roșii.

Pentru a evalua exactitatea:

- Clasa Minor corespunde datelor anormale, iar clasa Normal corespunde datelor normale.
- Accuratețea poate fi evaluată comparând clasificarea efectuată de autoencoder (pe baza pragurilor) cu etichetele reale.
- Pentru a obține o valoare numerică a acurateței, se pot folosi metrici cum ar fi precizia, recuperarea sau scorul F1, în funcție de cerințe. Acestea pot fi calculate folosind etichetele reale și predicțiile autoencoderului.


![image](https://github.com/mihaescurazvan/tournament/assets/83414814/4af9b71e-6964-4b98-a11d-80a191093fbc)

![image](https://github.com/mihaescurazvan/tournament/assets/83414814/d2beec9a-9d0b-493d-97d2-78ce0056cc0e)

![image](https://github.com/mihaescurazvan/tournament/assets/83414814/585036b8-ad30-48ce-89f3-09f81c61f84f)



Bibliografie: https://www.researchgate.net/publication/352142543_Variational_Autoencoders_and_Wasserstein_Generative_Adversarial_Networks_for_Improving_the_Anti-Money_Laundering_Process
              https://arxiv.org/pdf/2306.11586.pdf
              https://github.com/IBM/Multi-GNN/blob/main/models.py
