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
- `Model susu dan growth rate.xlsx`
    - Sample model for milk yield and body weight
- `Calcium.xlsx`
    - Highlighted parameters for Calcium Requirements
- `Pemakanan bahan kering(Dry matter intake).xlsx`
    - Highlighted parameters for DMI
- `Phosphorus.xlsx`
    - Highlighted parameters for Phosphorus
- `Protin.xlsx`
    - Highlighted parameters for CP
- `Tenaga Metabolisma.xlsx`
    - Highlighted parameters for ME

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

# Flow of system
 1. Calculate nutrient requirements for cattle. We need Calcium (C), Phosphorus (P), Dry Matter Intake (DMI), Crude Protein (CP), Metabolizable Energy (ME). These are calculated from cattle data.
     - Sheets: `NRC 2001-2016 req`
 2. Determine the distribution for each ingredient using the least cost solver to get the formulation. 
     - Sheets: `Least Cost`
 3. Determine how much formulation to give each cattle.
    - This is calculated by `total forage required` and `total concentrate required` in the second diagram.
    - Sum up total weight for each forage and concentrate required.
    - Sheets: `Rumusan pemberian makanan tepat`, `Slot 1`.

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

## Distributing feed amount
![Feed Amount Diagram](./feed-amount.drawio.svg)

[Edit this diagram](https://app.diagrams.net/?url=https://raw.githubusercontent.com/piperdd/MARDI-diagrams/main/feed-amount.drawio.svg)


# JF Model and Gompertz Model
## Purpose
Body Weight and Milk Yield readings are not taken every day. So, we use these models to estimate body weight/milk yield values for the days that readings are not taken.

## Milk Production Graph

File: `Model susu dan growth rate.xlsx`

JF Model (row 12 in `original/edited susu sheet`:
<img width="1024" height="96" alt="image" src="https://github.com/user-attachments/assets/4ffee44d-5d6a-46c7-a2c6-40b460070e4d" />

<img width="1543" height="516" alt="image" src="https://github.com/user-attachments/assets/7308c912-dcf5-4ffa-8a20-35bd556d96af" />

During Daily Input Data when we measure the milk yield, we need to calculate the ratio (nisbah pengeluaran).
The formula for the ratio is `Milk Yield / Value of JF Model at current day of milking`

For example:

A livestock produces 10kg of milk on the 50th day of milking, the value of the model at the 50th day is 22.4kg.
So the ratio is 10/22.4 = 0.446

We store this ratio alongside the milk yield input data:
| Days in Milking | Milk Yield (kg) | Ratio |
|---|---|---|
| 50 | 10 | 0.446 |
| 100 | 9 | 0.430 |
| ... | ... | ... |

From this, we calculate the average ratio. The average ratio will be used to get the adjusted graph.

## Obtaining value from adjusted graph
use formula:
estimated milk yield = average ratio * JF(current day in milking)

Example: 

We want to find the estimated milk yield for the 150th day.

The average ratio is (0.446+0.430)/2 = 0.438

The JF value for that day is JF(150) = 18.92

So, the estimated milk yield for 150th day = 0.438*18.92 = 8.287

[Experiment with graph](https://www.desmos.com/calculator/beaxlxqrc0)

## Body Weight Graph
The same procedure is done for estimating body weight.

Gompertz Model:
<img width="959" height="96" alt="image" src="https://github.com/user-attachments/assets/1945ae6c-b553-4a2b-a165-93935e97c5bb" />
<img width="996" height="104" alt="image" src="https://github.com/user-attachments/assets/17d4fad1-4d0b-4960-bd11-dc72a9b19c49" />



# Parameter untuk prestasi ladang

![Untitled](https://github.com/user-attachments/assets/f540a666-056b-43ad-8228-95538aa5cbcb)

## Parameters required

- Calving dates (setiap tarikh beranak)
- Conception dates (setiap tarikh mula mengandung)
    - Needs information whether Artificial Insemnation (AI) or Natural Breeding (to keep track of parent/breed) 
    - Needs information whether conception is successful or not (used by Days Open)
- Service dates (setiap tarikh insemination)
    - need to keep track date of first service (for AFS, CFSI)
    - first service means the first service after birthing a calf, not the first service in it's lifetime. So a cow can have multiple first services.

## Individual vs Group Data (Need confirmation)

Individual:
- CI
- DO
- S/C
- AFS
- AFC
- CFSI
- Abortion Rate
- Stillbirth Rate

Group:
- CR
- HDR
- PR
- NRR
- FSCR

Unsure:
- VWP - not sure if VWP is defined individually or for whole group

## Further Information

- Returning to estrus - if cow is inseminated but no conception, it will show signs of estrus (heat) again. If it doesnt return to estrus, it might mean that it has successfully conceived.
- Service - act of inseminating a cow.
- Service =/= Conception. Services can be successful/non successful. Successful service leads to conception.
- Abortion - calf aborted before expected birth date
- Stillbirth - calf is not alive during expected birth date


