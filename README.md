# MARDI-diagrams
for storing draw.io files

# Latest Documents
- `Model perumusan pemakanan dan simulasi pengeluaran lembu tenusu(Heifer)v6`
- `Model perumusan pemakanan dan simulasi pengeluaran lembu tenusu(Calf)v6`
- `Model perumusan pemakanan dan simulasi pengeluaran lembu tenusu(Steer)v6`
- `Model perumusan pemakanan dan simulasi pengeluaran lembu tenusuv11.11.2024 (v3)`
- `Model penggunaan sistem DSSv3`

# Groups of cattle
- Lembu Anak
    - Umur bawah 180 hari, selepas tempoh tersebut automatically masuk Heifer (Betina) atau Pejantan (Jantan)
- Lembu Pejantan
    - Lembu jantan berumur lebih 180 hari.
- Lembu Heifer
    - Lembu betina yang belum melahirkan anak pertama
    - Walaupun sedang mengandung, jangan masukkan ke lembu menyusu, hanya waktu dah  beranak akan masukkan ke lembu menyusu
- Lembu Menyusu
    - Lembu yang sedang menyusu.
    - Tidak kira mengandung atau tidak.
- Lembu Tidak Menyusu
    - Lembu yang sudah berhenti menyusu.
    - Perlu mengandung semula untuk mengeluarkan susu.

# Least Cost Formulation
## Information Required
- Ingredient nutrient values (ME, CP, Ca, P) (In `Feed database` sheet)
- Nutrient requirement per group (In `NRC 2001-2016 req` sheet)
    - Nutrient requirement depends on various factors:- (There may be more)
        - cattle weight
        - week of lactation
        - milk yield
        - milk fat
        - milk protein
        - calf birth weight (lookup values on breed table)
        - days in pregnancy

## Nutrient dependency diagram. (open in new tab for clearer view)
Purple - What is required by the solver (ME, CP, Ca, P)
Blue - Intermediate variable
Green - Data required from user/database (this is not dependent on any other factors)
![Nutrient Requirements Diagram](./nutrient-requirements.drawio.svg)

[Edit this diagram](https://app.diagrams.net/?url=https://raw.githubusercontent.com/piperdd/MARDI-diagrams/main/nutrient-requirements.drawio.svg)

