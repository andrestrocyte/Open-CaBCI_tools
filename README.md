# Open-CaBCI_tools

**Analysis tools to dissect population dynamics in calcium-based Brain-Computer Interface experiments. Companion package to [Open-CaBCI](https://github.com/donatolab/Open-CaBCI).**

---

## Overview

Open-CaBCI_tools provides binarization pipelines for converting continuous two-photon calcium imaging traces into binarized time series, enabling downstream analysis of population dynamics in BCI experiments.

---

## Associated Publication

**[Equivalent volitional learning emerges through circuit-specific population dynamics in motor cortex and hippocampus](https://www.biorxiv.org/content/10.64898/2026.06.04.730137v1)**

Andres de Vicente\*, Catalin Mitelut\*, Renan Viana Mendes, Lorenzo Marianelli, Mariona Colomer Rosell, David Bruckner, Giampiero Bardella, and Flavio Donato

\*Equal contribution | Correspondence: flavio.donato@unibas.ch

bioRxiv 2026.06.04.730137 | doi: [10.64898/2026.06.04.730137](https://www.biorxiv.org/content/10.64898/2026.06.04.730137v1)

> 📢 **If you use Open-CaBCI_tools in your research, please cite the above publication.**

---

## Requirements

- Python 3.x
- Two `.yaml` metadata files per recording:
  - `ANIMAL_ID.yaml` — inside the animal directory
  - `SESSION_ID.yaml` — inside the session directory

Please see the example `.yaml` files provided in the repository.

---

## Installation

```bash
pip install -r requirements.txt
```

---

## Usage

```python
from binarize2pcalcium import binarize2pcalcium as binca

data_dir = '/media/cat/2pdata'
animal_id = 'DON-011733'
session = '20230203'

c = binca.Calcium(data_dir, animal_id)

c.session = session
c.session_name = session

c.data_type = '2p'
c.remove_bad_cells = False
c.verbose = False                        # outputs additional information during processing
c.recompute_binarization = True          # recomputes binarization; False: loads from previous saved locations

# set flags to save output
c.save_python = True                     # save output as .npz file
c.save_matlab = False                    # save output as .mat file

# spike detection thresholds
c.dff_min = 0.05                         # min %DFF for [ca] burst to be considered a spike (default 5%)
c.percentile_threshold = 0.9999          # threshold for [ca] bursts outside noise floor
c.maximum_std_of_signal = 0.08           # signals with std above this are flagged as noisy

c.binarize_data()
```

---

## Repository Structure

```
Open-CaBCI_tools/
├── bmitools/         # Core analysis tools
├── .vscode/          # Editor settings
├── MANIFEST.in       # Package manifest
├── setup.py          # Installation script
├── LICENSE           # GPL-3.0 license
└── README.md
```

---

## Credits

This repository builds on tools originally developed by **Catalin Mitelut** ([@catubc](https://github.com/catubc/bmi_tools)). We are grateful for his foundational contributions.

---

## License

This project is licensed under the [GPL-3.0 License](https://github.com/donatolab/Open-CaBCI_tools#GPL-3.0-1-ov-file).

---

## Contact

**Donato Lab** | Biozentrum, University of Basel
🌐 [donatolab.com](https://www.donatolab.com) | ✉️ flavio.donato@unibas.ch
