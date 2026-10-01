# solar_energy_generation

Client proposal: whether installing a battery is cost effective for a household with
solar panels, based on hourly 2020 generation and usage data.

## Files

| File | Contents |
| --- | --- |
| `solar_energy.ipynb` | The model. Data checks, outlier corrections, hourly battery simulation, NPV and IRR. |
| `solar_energy_data.csv` | Hourly solar generation and household usage for 2020 (8,760 rows). |
| `report.pdf` / `report.odt` | Client-facing write-up of the findings. |
| `ode.ipynb` | Unrelated file, left over from another project. Safe to delete. |

## Headline result

The battery supplies an extra **3,498.61 kWh per year**, worth **$594.76** at the
1 January 2022 tariff of $0.17/kWh. Against the $7,000 cost over a 20-year life:

| Scenario | NPV (net of cost) | IRR | Discounted payback |
| --- | --- | --- | --- |
| Prices rise 4% p.a. | $2,420.98 | 9.42% | year 15 (2036) |
| Prices rise 4% + 0.25pp p.a. | $3,730.60 | 10.70% | year 14 (2035) |

Both clear the 6% discount rate, so the investment is worthwhile &mdash; but only if
electricity prices rise. Held flat at $0.17/kWh the NPV is **-$178.11** and the IRR
5.68%, below the hurdle.

Two qualifications belong with that recommendation, both quantified in the notebook:

- **39% of solar generation is wasted** because the battery is already full for 1,087
  hours a year. A smaller battery captures much of the same benefit for less money.
- **The supplied usage data is not characteristic of a household** &mdash; ~49.6 kWh/day
  with peaks of 61 kW. This limits confidence in the absolute dollar figures, though it
  does not change the conclusion.

## Reproducing the analysis

Requires the `data_sciences` conda environment.

```bash
conda activate data_sciences
jupyter nbconvert --to notebook --execute solar_energy.ipynb
```

All self-checks are `assert` statements, so execution fails loudly if the data or the
model regresses rather than silently producing numbers.
