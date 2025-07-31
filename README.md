# MARDI-diagrams
for storing draw.io files

# Latest Documents
- `Model perumusan pemakanan dan simulasi pengeluaran lembu tenusu(Heifer)v6.xlsm`
    - For Lembu Heifer
- `Model perumusan pemakanan dan simulasi pengeluaran lembu tenusu(Calf)v6.xlsm`
    - For Lembu Anak
- `Model perumusan pemakanan dan simulasi pengeluaran lembu tenusu(Steer)v6.xlsm`
    - For Lembu Pejantan
- `Model perumusan pemakanan dan simulasi pengeluaran lembu tenusuv11.11.2024 (v3).xlsm`
    - For Lembu Menyusu/Tidak Menyusu
- `Model penggunaan sistem DSSv3.pptx`
    - Slides

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

## Milk Production Graph

Sheet: `Pendaftaran ternakan` and `Data pemakanan baru`

<img width="1543" height="516" alt="image" src="https://github.com/user-attachments/assets/7308c912-dcf5-4ffa-8a20-35bd556d96af" />

For each livestock in a group, we need to calculate the ratio (nisbah pengeluaran).
The formula for the ratio is `Milk Yield / Value of Model at current day of milking`

For example:

A livestock produces 10kg of milk on the 50th day of milking, the value of the model at the 50th day is 22.4kg.
So the ratio is 10/22.4 = 0.446

Once we get all ratios of each livestock in group, calculate the average.The average will then be used for the value of 'r' in the graph above.

[Experiment with graph](https://www.desmos.com/calculator/beaxlxqrc0)

## Parameter untuk prestasi ladang

![Untitled](https://github.com/user-attachments/assets/f540a666-056b-43ad-8228-95538aa5cbcb)

