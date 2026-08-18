# Reuters C50 — Klasifikacija autora novinskih tekstova

Seminarski rad u okviru kursa **Istraživanje podataka 2**, Matematički fakultet.

Cilj projekta je klasifikacija autora novinskih članaka (Reuters C50 dataset, 50 autora,
5000 tekstova) na osnovu sadržaja teksta, korišćenjem TF-IDF vektorizacije i sedam
klasifikacionih algoritama nad tri različita skupa atributa (21 model ukupno).

## Struktura projekta

```
ip2Projekat/
├── data/
│   ├── C50train/                  sirovi tekstualni fajlovi po autoru (trening)
│   ├── C50test/                   sirovi tekstualni fajlovi po autoru (test)
│   ├── reuters_raw.csv            učitan dataset (generiše notebook 01)
│   ├── reuters_preprocessed.csv   preprocesirani tekst (generiše notebook 02)
│   └── rezultati_klasifikacije.csv rezultati svih 21 modela (generiše notebook 04)
├── notebooks/
│   ├── 01_ucitavanje_podataka.ipynb
│   ├── 02_preprocesiranje.ipynb
│   ├── 03_vizualizacija_2d_3d.ipynb
│   ├── 04_klasifikacija.ipynb
│   └── 05_evaluacija.ipynb
├── slike/                         grafici generisani iz notebook-a (20 slika)
├── dokumentacija.tex              tekstualni deo rada (izvor)
├── dokumentacija.pdf              tekstualni deo rada (kompajliran)
├── requirements.txt
└── README.md
```

## Priprema okruženja

Potreban je Python 3.10+.

```bash
python3 -m venv jupyter-env
source jupyter-env/bin/activate
pip install -r requirements.txt
```

Prilikom prvog pokretanja notebook-a `02_preprocesiranje.ipynb`, NLTK će automatski
preuzeti resurse `stopwords` i `punkt` (potrebna internet konekcija).

## Redosled pokretanja

Notebook-e je potrebno pokrenuti **redom, od 01 do 05**, iz `notebooks/` foldera —
svaki naredni notebook koristi izlaz prethodnog (relativne putanje su `../data`,
`../slike`, u odnosu na `notebooks/`).

| Notebook | Šta radi | Izlaz |
|---|---|---|
| `01_ucitavanje_podataka.ipynb` | Učitava sirove tekstove iz `data/C50train`, `data/C50test`, osnovna eksploracija (dužina teksta, balansiranost klasa) | `data/reuters_raw.csv`, slike `01`–`03` |
| `02_preprocesiranje.ipynb` | Čišćenje teksta, uklanjanje stop-reči, stemovanje (Porter Stemmer), word cloud | `data/reuters_preprocessed.csv`, slike `04`–`06` |
| `03_vizualizacija_2d_3d.ipynb` | TF-IDF → SVD → PCA/t-SNE, 2D i 3D vizualizacija dokumenata po autoru | slike `07`–`11` |
| `04_klasifikacija.ipynb` | TF-IDF (3 skupa atributa: 10 000 / 2 000 / 500), treniranje 7 klasifikatora (21 model) | `data/rezultati_klasifikacije.csv`, slike `12`–`14` |
| `05_evaluacija.ipynb` | Detaljna evaluacija najboljeg modela (SVM): confusion matrica, classification report, cross-validacija, analiza po autorima | slike `15`–`20` |

Napomena: notebook `03` (t-SNE) i `04` (treniranje 21 modela) mogu trajati nekoliko
minuta.

## Dataset

Reuters C50, UCI Machine Learning Repository:
https://archive.ics.uci.edu/dataset/217/reuter+50+50

## Dokumentacija

Detaljan opis podataka, obrade i rezultata nalazi se u `dokumentacija.pdf`
(izvor: `dokumentacija.tex`).

## Autor

Zagorka Pantović — mi20227@alas.matf.bg.ac.rs
