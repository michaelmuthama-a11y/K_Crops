# Kenya Crops Power BI Dashboard — README

## Dataset
500 farmer-season records, 20 source columns.

## Cleaning
There are 668 affected cells across the six required categorical columns:
Season 56; Crop Variety 44; Soil Type 50; Irrigation Method 163; Fertilizer Used 152; Pest Control 203.

`Error` and `N/A` are mapped to `Unknown`. Blanks in Season, Crop Variety and Soil Type are `Unknown`. Blanks in Irrigation Method, Fertilizer Used and Pest Control are `None` because `None` is a valid category in the data dictionary.

Farmer Contact remains Text. Numeric columns are Decimal Number. Planting Date and Harvest Date are Date.

## Revenue and profit validation
429 rows have Yield, Market Price and Revenue present. The dataset matches **Planted Area × Yield × Market Price** for all 429, not Yield × Market Price alone. This indicates the assignment wording omitted planted area.

404 complete Revenue/Cost/Profit rows all satisfy Profit = Revenue − Cost within 0.01 KES.

Missing Revenue is reconstructed only when Area, Yield and Market Price are all available. Missing Profit is reconstructed only when cleaned Revenue and Cost are available.

## Model
- Fact: kenya_crops
- Date dimension: Date Table
- Relationship: Date Table[Date] 1:* kenya_crops[Planting Date]
- Date table covers 1 Jan 2023 to 31 Dec 2023 and is marked as a date table.
- Region mapping: West = Kisumu/Eldoret/Kericho; East = Meru/Machakos/Mombasa; Central = Nairobi/Nyeri/Nakuru/Kiambu.

## Dashboard pages
1. Overview KPIs
2. Crop and County Performance
3. Farming Practices
4. Revenue Over Time

Recommended slicers: County, Crop Type, Season.

## Key findings
- Highest observed crop/county profit per acre: Beans — Mombasa, KES 746,828.21/acre.
- Lowest observed negative crop/county profit per acre: Beans — Meru, KES -11,137.15/acre.
- Average profit is higher for Drip than None in the raw data: KES 3.137M vs KES 2.222M per record.
- CAN has the highest average profit among named fertilizer categories: KES 3.266M per record.

These are descriptive associations, not causal estimates.

## Recommendations
1. Investigate high-value crop/county combinations using profit per acre plus sample size and total profit.
2. Investigate irrigation performance, especially Drip versus non-irrigated plots, controlling for crop/county.
3. Review fertilizer choice together with input cost, yield and profit margin before scaling any practice.

## PBIX
The `.pbix` file must be assembled in Power BI Desktop. The accompanying `.m` Power Query script and DAX answer sheet provide the implementation.
