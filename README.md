
# MTB Genotype and Drug Resistance Summary Script

This Bash script automates the detection and summary of **Mycobacterium tuberculosis (MTB)** genotypes and associated drug resistance markers from a set of result files. It is tailored for samples analyzed using genotype and resistance profiling tools and identifies specific mutations and gene markers relevant to Ugandan MTB strains and drug resistance.

---

## What It Does

For each sample listed in `list.txt`, the script:

- Detects presence of **MTB Uganda lineage** markers (general, Uganda I, Uganda II).
- Checks for resistance mutations associated with the following anti-TB drugs:
  - **Rifampicin**
  - **Ethambutol**
  - **Fluoroquinolones** (e.g., Ofloxacin, Moxifloxacin, Ciprofloxacin)
  - **Streptomycin**
  - **Kanamycin**
  - **Amikacin & Capreomycin**
  - **Pyrazinamide**
  - **Isoniazid**

The script outputs a summary interpretation file for each sample, named:
```
<SAMPLE>.Summary-and-Interpretation-of-UG-MTB-Genotype-and-Drug_resistance.txt
```

---

## Input Files

- `list.txt`: A text file containing one sample name per line (without file extensions).
- For each sample, a corresponding result file must be present:
  ```
  <SAMPLE>.Details-of-UG-MTB-Genotype-and-Drug_resistance.txt
  ```

---

## How to Run

Make sure the script is executable:
```bash
chmod +x mtb_genotype_summary.sh
```

Then run the script:
```bash
./mtb_genotype_summary.sh
```

---

## Output

For each sample in `list.txt`, a summary file will be created highlighting:

- Lineage detection (e.g., MTB Uganda I, MTB Uganda II)
- Detected drug resistance mutations by gene or mutation type

Example output content:
```
MTB Uganda Detected
MTB Uganda II Detected
Rifampicin Resistance Detected
Isoniazid Resistance Detected
```

---

## Genes & Mutations Monitored

| Drug                  | Genes / Mutations Checked                     |
|-----------------------|-----------------------------------------------|
| **Rifampicin**        | `rpoB`                                        |
| **Ethambutol**        | `embA`, `embB`, `embC`, `embR`, `iniA`, `iniC`, `manB`, `rmlD` |
| **Fluoroquinolones**  | `gyrA`                                        |
| **Streptomycin**      | `rpsL`                                        |
| **Kanamycin**         | `eis`                                         |
| **Amikacin/Capreomycin** | `gidB`, `rrs`, `tlyA`                     |
| **Pyrazinamide**      | `pncA`, `rpsA`                                |
| **Isoniazid**         | `ahpC`, `fabG1`, `inhA`, `katG`, `ndh`       |

---

## Notes

- Ensure all `.Details-of-UG-MTB-Genotype-and-Drug_resistance.txt` files are present in the same directory as the script.
- The script assumes specific variant IDs (`p.Thr80Ala`, `7539`, etc.) for MTB Uganda lineage detection.

---

## License

This script is provided under the MIT License.
