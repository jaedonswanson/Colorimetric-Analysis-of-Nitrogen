# Colorometric Analysis of Inorganic Nitrogen
This repository should contain everything needed to get started running freshwater samples for inorganic nitrogen through colorometric methods on a microplate (elx800) or similar. This is an efficient and inexpensive method of measuring nutrient concentration in water, resin, or soil extracts.

**A note on sample collection:** When collecting water samples, they should be filtered through a 0.45 micron filter. If the samples cannot be processed the same day, freeze or acidify them to prevent deterioriation.

## Part 1: Running the experiment
**NOTE:** Double check the required chemicals; not all are needed if only running one type of samples (water, resin, soil).

1. Follow the relevant procedure:
   - [Ammonium](Procedures/Micoplate%20Anlaysis%20of%20Ammonium.md)
   - [Nitrate & Nitrite](Procedures/Microplate%20Analysis%20of%20Nitrate%20&%20Nitrite.md)
2. Set up an Excel file to act as a key for the sample locations.
   1. If not formatted like [this key](Plates/nitrate_key.xlsx), the code following this will break as is.
3. After the appropriate incubation time, analyze the plate.
   - If using Gen 5 software from BioTek you can load `Inoragnic-Nitrogen-Protocol.prt`
4. After the plate is run, copy the data to a `.csv` and name it:
   - [MMDDYYYY_nutrient_replication](Plates/Nitrate/)
      - This is essential to make sure the plate ID matches the corresponding key.
        - `01012027_nitrate_1.csv`
  
## Part 2: Assessing the Standards
1. Open the [standard checking](Standard-Checking.qmd) and update the relevant information at the top.
2. Run the script and examine the graphs & $r^2$ value.
   - Ideally, all standards produce an $r^2$ ≥ 0.98.
3. If $r^2$ is < 0.98, examine the graph and remove problem standard(s).
   - **Notes:**
      - If possible, do not remove a standard that best approximates sample concentration.
      - If you have to remove more than 3 standards (only 5 points remaining), something likely went wrong and you should start over.
## Part 3: Calculating concentrations
1. Open the [concentration calculation](concentration_calculation.qmd) script.
2. Update the information to exactly match the settings from above (e.g., plate ID, removed standards).
3. Run the script.
4. It should output a file with the concentrations of your samples to `Concentrations/Nutrient`

## Part 4: Tidying
1. Whenever you want a clean file of your data, run the [tidying script](tidying.qmd).
   1. **Note:** Make sure to update site names and output paths to reflect your desired output.

## Emphasizing the importance formating the key

The `nitrate_key.xlsx` and `nitrite_key.xlsx` files are examples. Each workbook must use:
- One worksheet for each plate.
- A worksheet name matching the plate filename's date and replication:
  `MMDDYYYY_replication` (for example, `01012027_1`).
- A first column named `Row` containing `A` through `H`.
- Twelve additional columns named `1` through `12`.
- Sample IDs in the cells corresponding to their wells. Repeated sample IDs
  represent technical replicates and are numbered automatically.

For a plate named `01012027_nitrite_1.csv`, the calculation script reads the `01012027_1` worksheet from `nitrite_key.xlsx`. The row and column labels are joined to the plate CSV coordinates, so the layout must match the physical plate exactly.