<div align="center">

# 🔐 BB84 Quantum Key Distribution — Simulazione

**Simulazione del protocollo BB84 con Qiskit per la distribuzione sicura di chiavi quantistiche**

[![Python](https://img.shields.io/badge/Python-3.10%20%7C%203.11%20%7C%203.12-blue.svg)](https://www.python.org/)
[![Qiskit](https://img.shields.io/badge/Qiskit-1.x-6929C4.svg)](https://qiskit.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![Contributors](https://img.shields.io/badge/Contributors-3-brightgreen.svg)](#-autori)

</div>

---

## 👥 Autori

Progetto sviluppato come lavoro di gruppo da:

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/TUO-USERNAME">
        <img src="https://github.com/Nolek88.png" width="100px;" alt="Alessandro Romeo"/><br />
        <sub><b>Alessandro Romeo</b></sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/DavideTorelli">
        <img src="https://github.com/GITHUB-DAVIDE.png" width="100px;" alt="Davide Torelli"/><br />
        <sub><b>Davide Torelli</b></sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/GITHUB-SIMONE">
        <img src="https://github.com/SimoVia00.png" width="100px;" alt="Simone Viatore"/><br />
        <sub><b>Simone Viatore</b></sub>
      </a>
    </td>
  </tr>
</table>

---

## 📖 Descrizione

Questo progetto implementa una **simulazione dettagliata del protocollo BB84**, il primo e più celebre protocollo di **Quantum Key Distribution (QKD)**, sviluppato da Bennett e Brassard nel 1984.

L'obiettivo è duplice:

1. **Dimostrare** come Alice e Bob possano stabilire una chiave segreta condivisa sfruttando le leggi della meccanica quantistica.
2. **Analizzare** la robustezza del protocollo in presenza di un attacco *intercept-resend* (Eve) e di rumore hardware realistico (canale depolarizzante).

La sicurezza del BB84 non si basa sulla difficoltà computazionale di un problema matematico (come RSA o ECC), ma su **principi fisici fondamentali**:

- 🚫 **Teorema di no-cloning**: non è possibile copiare uno stato quantistico sconosciuto.
- 👁️ **Effetto dell'osservatore**: misurare un qubit ne disturba lo stato, rendendo ogni spionaggio rilevabile.

---

## ✨ Funzionalità

- ✅ Preparazione degli stati quantistici di **Alice** (bit + base casuale)
- ✅ Misurazione di **Bob** (base casuale)
- ✅ **Sifting** — confronto delle basi sul canale classico
- ✅ Stima del **QBER** (Quantum Bit Error Rate)
- ✅ Simulazione dell'**attacco intercept-resend di Eve**
- ✅ Simulazione del **rumore hardware** (canale depolarizzante)
- ✅ **Grafici comparativi** dell'effetto di Eve e del rumore

---

## 🗂️ Struttura del progetto

```text
bb84-qkd-simulation/
├── README.md
├── LICENSE
├── .gitignore
├── requirements.txt
├── BB84_QKD_Simulation.ipynb      # Notebook principale
├── docs/
│   └── Sicurezza_nell_Era_Quantistica.pdf
└── results/
    └── risultati_algo.txt
```

---

## ⚙️ Installazione

### 1. Clona il repository

```bash
git clone https://github.com/TUO-USERNAME/bb84-qkd-simulation.git
cd bb84-qkd-simulation
```

### 2. Crea un ambiente virtuale (consigliato)

```bash
python -m venv .venv

# Linux / macOS
source .venv/bin/activate

# Windows (PowerShell)
.venv\Scripts\Activate.ps1
```

### 3. Installa le dipendenze

```bash
pip install -r requirements.txt
```

---

## 🚀 Uso

Avvia Jupyter Lab (o Jupyter Notebook):

```bash
jupyter lab
```

Apri il notebook `BB84_QKD_Simulation.ipynb` ed esegui le celle in ordine.

Il notebook è organizzato in sezioni:

1. **Import e configurazione**
2. **Utility BB84** (preparazione stati)
3. **Costruzione del circuito quantistico**
4. **Simulazione e sifting**
5. **Calcolo del QBER**
6. **Attacco di Eve**
7. **Modello di rumore hardware**
8. **Generazione dei grafici**

---

## 📊 Risultati

Di seguito i risultati ottenuti su **256 bit iniziali** (chiave filtrata ≈ 135 bit).

### Scenario 1 — Canale ideale (baseline)

| Metrica | Valore |
|---|---|
| Eve | ❌ Assente |
| Rumore | ❌ Assente |
| Chiave filtrata | **135 bit** (~50%) |
| Errori | 0 |
| **QBER** | **0.00%** |
| Esito | ✅ SUCCESSO — chiave perfetta |

---

### Scenario 2 — Attacco di Eve (intercept-resend 100%)

| Metrica | Valore |
|---|---|
| Eve | ☠️ Presente (100%) |
| Rumore | ❌ Assente |
| Errori | 32 |
| **QBER** | **≈ 23.70%** |
| Soglia di sicurezza | 11% |
| Esito | 🚨 RILEVATO — chiave scartata |

> Il QBER osservato è **vicino al limite teorico del 25%** previsto per l'attacco intercept-resend. Il protocollo ha **rilevato con successo l'intrusione**.

---

### Scenario 3 — Canale rumoroso (p = 5%)

| Metrica | Valore |
|---|---|
| Eve | ❌ Assente |
| Rumore | ⚡ Presente (depolarizzante p = 5%) |
| Chiave filtrata | 128 bit |
| Errori | 3 |
| **QBER** | **≈ 2.34%** |
| Esito | ✅ SUCCESSO — chiave sicura post-correzione |

---

## 📈 Grafici

Il notebook genera due grafici comparativi:

- **QBER vs Tasso di intercettazione di Eve**
  Il QBER cresce linearmente come `QBER = 0.25 × r`, seguendo la predizione teorica. Superata la soglia dell'11% (≈ 44% di intercettazione), l'attacco diventa palese.

- **QBER vs Livello di rumore hardware**
  Anche il rumore depolarizzante introduce errori in modo **lineare**. Il fit fornisce `y ≈ 0.71x`. Se `p > ~0.08`, il QBER supera l'11% **anche in assenza di Eve**, rendendo la comunicazione non sicura.

---

## 🧠 Background teorico

Il protocollo BB84 si articola in 4 fasi:

| Fase | Chi | Cosa fa |
|---|---|---|
| 1️⃣ Invio | Alice | Invia qubit polarizzati in 4 stati (2 basi × 2 bit) |
| 2️⃣ Misura | Bob | Misura scegliendo casualmente base Z o X |
| 3️⃣ Sifting | Entrambi | Confrontano le basi; scartano i bit discordanti |
| 4️⃣ QBER | Entrambi | Sacrificano parte della chiave per stimare gli errori |

Se il QBER supera la **soglia di sicurezza (~11%)**, il protocollo viene abortito.

---

## 🛠️ Tecnologie utilizzate

| Libreria | Ruolo |
|---|---|
| [Qiskit](https://qiskit.org/) | Costruzione e simulazione dei circuiti quantistici |
| [Qiskit Aer](https://qiskit.org/ecosystem/aer/) | Simulatore quantistico + modelli di rumore |
| [NumPy](https://numpy.org/) | Generazione casuale e calcoli numerici |
| [Matplotlib](https://matplotlib.org/) | Visualizzazione dei risultati |
| [Jupyter](https://jupyter.org/) | Ambiente di sviluppo interattivo |

---

## 🤝 Contributi

Contributi, segnalazioni di bug e suggerimenti sono benvenuti!

1. Fai un **fork** del progetto
2. Crea un **branch** (`git checkout -b feature/nuova-funzionalita`)
3. Fai il **commit** (`git commit -m "Aggiunge nuova funzionalità"`)
4. Fai il **push** (`git push origin feature/nuova-funzionalita`)
5. Apri una **Pull Request**

---

## 📜 Licenza

Questo progetto è distribuito sotto licenza **MIT**. Vedi il file [LICENSE](LICENSE) per i dettagli.

---

## 📚 Riferimenti

- Bennett, C. H., & Brassard, G. (1984). *Quantum cryptography: Public key distribution and coin tossing*. Proceedings of IEEE International Conference on Computers, Systems and Signal Processing.
- Nielsen, M. A., & Chuang, I. L. (2010). *Quantum Computation and Quantum Information*. Cambridge University Press.
- [Qiskit Documentation](https://docs.quantum.ibm.com/)

---

<div align="center">

**⭐ Se questo progetto ti è stato utile, lascia una stella su GitHub! ⭐**

<br />

Realizzato da <a href="https://github.com/TUO-USERNAME">Alessandro Romeo</a>, <a href="https://github.com/GITHUB-DAVIDE">Davide Torelli</a> e <a href="https://github.com/GITHUB-SIMONE">Simone Viatore</a>

</div>
