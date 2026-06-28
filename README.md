# Investigating Kasios's Rose-Crested Blue Pipit Claim

This project investigates VAST Challenge 2018 Mini-Challenge 1, where Kasios Office Furniture claims that its recent bird recordings prove Rose-crested Blue Pipits are still thriving across the Boonsong Lekagul Wildlife Preserve.

The analysis combines two lines of evidence:

1. Spatial and temporal visualization in Tableau.
2. Spectral audio analysis of verified Pipit recordings versus Kasios recordings.

The central question is:

> Are the birds Kasios claims are Rose-crested Blue Pipits actually consistent with verified Rose-crested Blue Pipit recordings?

## Interactive Tableau Exploration

View the spatial-temporal Tableau story here: [Tableau Public - Wildlife Claims Analysis](https://public.tableau.com/views/ridma_tableau/Story1?:language=en-GB&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

## Project Story

The first phase explored the verified bird metadata and Kasios test bird locations in Tableau using `ridma_tableau.twbx`. The Tableau dashboards combine:

- `AllBirdsv4.csv`: verified bird recording metadata from the observatory.
- `updated_AllBirdsv4.xlsx`: cleaned bird metadata used during analysis.
- `Test Birds Location.csv`: locations of the recordings supplied by Kasios.
- `Lekagul Roadways 2018.bmp`: the preserve map used as the spatial background.

The spatial-temporal dashboards show that verified Rose-crested Blue Pipit recordings decrease over time, especially after 2015. The dashboards also show that verified Pipits have not appeared in or near the suspected dumping site since 2015, while many of the birds Kasios claims are Pipits are located in that area.

Important note: the challenge data description lists the suspected dumping site as `(148,40)`, but this project treats that coordinate as incorrect for the working map interpretation. The Tableau map indicates the suspected dumping site near `(148,160)`.

This raised the key investigative question: if Kasios's birds are located where verified Pipits have not been seen recently, are those birds actually Rose-crested Blue Pipits?

## Audio Analysis

The second phase examined the bird recordings themselves.

The raw MP3 recordings are stored locally in two folders:

- `all_birds/`: verified bird recordings.
- `kasios_birds/`: recordings supplied by Kasios.

Because these folders are large, they are intentionally excluded from GitHub. See [DATA.md](DATA.md) for details.

The notebooks generate spectrograms and extract summary spectral statistics:

- `VAST_verified.ipynb`: processes verified Pipit recordings from `all_birds/`.
- `VAST_kaisos.ipynb`: processes Kasios recordings from `kasios_birds/`.
- `vast_spectral_stat_comparison.ipynb`: compares verified Pipit and Kasios spectral statistics.

Generated outputs include:

- `pipit_spectral_statistics.csv`
- `kasios_spectral_statistics.csv`
- `spectral_plots/` with generated spectrogram images

The `spectral_plots/` folder is also excluded from GitHub because it is a large generated-output directory. The statistics CSV files are small enough to include and preserve the core comparison.

## Methods

For each recording, the analysis extracted spectral features such as:

- Peak frequency
- Mean frequency
- Total magnitude
- Spectral entropy

The project then compared verified Pipit recordings against Kasios recordings using:

- Box plots
- Histograms
- Scatter plots
- Independent t-tests

These comparisons show visible and statistical differences between the verified Pipit recordings and the recordings supplied by Kasios.

## Findings

The evidence does not strongly support Kasios's claim.

The spatial analysis shows that verified Rose-crested Blue Pipits decline over time and are absent from the suspected dumping-site region after 2015. In contrast, Kasios's claimed Pipit recordings are concentrated around that suspicious area.

The spectral analysis also suggests that the Kasios recordings may not match verified Rose-crested Blue Pipit recordings. The distributions of several spectral features differ between the two groups, and the visualizations from the comparison notebook support the conclusion that Kasios's recordings may include birds that are not verified Pipits.

Overall, the project suggests that Kasios's claim should be treated with skepticism and investigated further.

## Repository Contents

```text
.
├── README.md
├── DATA.md
├── requirements.txt
├── 2018 MC1.pdf
├── Data Description.docx
├── AllBirdsv4.csv
├── updated_AllBirdsv4.xlsx
├── Test Birds Location.csv
├── Lekagul Roadways 2018.bmp
├── ridma_tableau.twbx
├── VAST_verified.ipynb
├── VAST_kaisos.ipynb
├── vast_spectral_stat_comparison.ipynb
├── pipit_spectral_statistics.csv
└── kasios_spectral_statistics.csv
```

Local-only folders not committed to GitHub:

```text
all_birds/
kasios_birds/
spectral_plots/
```

## How to Reproduce

1. Clone this repository.
2. Install the Python dependencies:

```bash
pip install -r requirements.txt
```

3. Place the raw audio folders at the project root:

```text
all_birds/
kasios_birds/
```

4. Run the notebooks in this order:

```text
VAST_verified.ipynb
VAST_kaisos.ipynb
vast_spectral_stat_comparison.ipynb
```

5. Open `ridma_tableau.twbx` in Tableau to review the spatial and temporal dashboards.

## Limitations

This analysis is exploratory. Spectral statistics are useful evidence, but they are not a full supervised bird-call classifier. A stronger follow-up would train and validate a classifier using verified labeled calls, then apply that classifier to the Kasios recordings.

Spatial and temporal patterns may also be affected by sampling practices, recorder placement, and yearly variation. The findings should therefore be interpreted as evidence that Kasios's claim is questionable, not as a final biological census of the preserve.

## Suggested Next Steps

- Add selected dashboard screenshots and comparison plots to a small `figures/` folder.
- Train a machine learning classifier using verified bird calls.
- Compare Kasios recordings against all known bird species, not only verified Pipits.
- Reconcile the challenge coordinate system with the Tableau map and document the dumping-site coordinate correction visually.
