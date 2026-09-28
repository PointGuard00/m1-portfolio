# Portfolio projekata iz mašinskog učenja

Projekti prediktivnog modelovanja u Python-u koji pokrivaju ceo proces: čišćenje podataka, statističke testove, izbor atributa, podešavanje modela kros validacijom i evaluaciju metrikama koje odgovaraju poslovnom problemu.

**Autor:** Uroš Vasilić, Fakultet organizacionih nauka, Univerzitet u Beogradu, smer Informacioni sistemi i tehnologije

## Projekti

| # | Projekat | Problem | Model | Ključni rezultat |
|---|----------|---------|-------|------------------|
| 1 | [Odlazak klijenata (churn)](01_odlazak_klijenata_stablo_odlucivanja.ipynb) | Koji klijenti banke će otići? | Stablo odlučivanja sa podrezivanjem | ROC-AUC 0,82; izborom praga recall za klijente koji odlaze povećan sa 50% na 60% |
| 2 | [Hit pesme na Spotify-ju](02_hit_pesme_knn.ipynb) | Da li će pesma biti u gornjih 25% po slušanjima? | k najbližih suseda (kNN) | Tačnost 89,5%, F1 za hitove 0,78 |
| 3 | [Nutritivne vrednosti brze hrane](03_brza_hrana_linearna_regresija.ipynb) | Predviđanje količine proteina | Linearna regresija (OLS) | R² 0,81, kompletna dijagnostika i VIF |
| 4 | [Dijagnoza raka dojke](04_rak_dojke_neuronska_mreza.ipynb) | Benigni ili maligni tumor? | Neuronska mreža (MLP) | Tačnost 97,4%, ROC-AUC 0,996 |

## Najvažnije

**1. Odlazak klijenata:** poslovno najrelevantniji projekat
- Neuravnotežene klase (oko 21% klijenata odlazi): bazni model ima tačnost 79%, ali ne pronalazi nijednog klijenta koji odlazi. Zato se modeli porede po ROC-AUC i recall-u, a ne po tačnosti.
- Izbor atributa potvrđen statističkim testovima (Mann-Whitney U, hi-kvadrat).
- Parametar podrezivanja (`ccp_alpha`) podešen stratifikovanom 10-strukom kros validacijom.
- Analiza praga odlučivanja: koliko klijenata koji odlaze pronalazimo, a koliko klijenata ukupno označavamo.

**2. Hit pesme na Spotify-ju**
- Shapiro-Wilk testovi za izbor načina zamene nedostajućih vrednosti i skaliranja (RobustScaler za asimetrične podatke sa outlierima).
- Skaliranje unutar scikit-learn `Pipeline`-a, tako da obrada podataka nikad ne vidi test skup (nema curenja podataka).
- Broj suseda k izabran stratifikovanom 10-strukom kros validacijom.

**3. Nutritivne vrednosti brze hrane (linearna regresija)**
- OLS regresija u statsmodels-u, tumačenje koeficijenata i njihove značajnosti.
- Dijagnostički grafici: reziduali naspram predviđenih vrednosti, Q-Q grafik, scale-location, Cook-ova distanca.
- Otkrivena i uklonjena multikolinearnost pomoću VIF.

**4. Dijagnoza raka dojke (neuronska mreža)**
- Višeslojni perceptron arhitekture 30-64-32-1 treniran SGD algoritmom.
- Objašnjenje zašto je u medicini najvažniji recall za maligne tumore.

## Tehnologije
Python, pandas, NumPy, scikit-learn, statsmodels, SciPy, matplotlib, seaborn

## Pokretanje
```bash
pip install -r requirements.txt
jupyter notebook
```
Skupovi podataka se nalaze u folderu `data/`.

## Sledeći koraci
- Poređenje modela za odlazak klijenata sa logističkom regresijom, Random Forest-om i XGBoost/LightGBM modelima
- Praćenje eksperimenata u MLflow-u
- Objašnjavanje pojedinačnih predikcija pomoću SHAP vrednosti
