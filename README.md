# Abstract 

Based on insights from previous years, our hypothesis is that incorporating additional weather information is critical for improving prediction precision. To that end, we leveraged historical weather data – including the daily maximum, mean, and minimum temperatures, daylight duration, precipitation sum, rain sum, and snowfall sum – collected from October to March for each year. In the specific case of 2025, since the March values were unavailable, we imputed these missing observations using estimates scraped from reputable weather forecasting websites. This enriched weather data was further processed via a custom function, which generated a comprehensive set of derived features capturing temporal trends and interactions.
Beyond weather, our feature engineering extended to the creation of lag features of the bloom day-of-year (bloom_doy) for every location and the construction of interaction variables. To mitigate potential issues associated with historical regime shifts – as documented by Reid et al., (2019), who reported a significant change in peak blossom timings around 1980 – we restricted our dataset to observations from the year 2000 onwards. This decision was supported by further evidence of pronounced shifts in recent decades, underscoring the need for a more recent and stable training period.
To capture the complex, non-linear relationships inherent in the data, we constructed an ensemble of diverse models. Our ensemble combined four different approaches: Support Vector Regression (SVR), Bayesian Ridge Regression, XGBoost, and LightGBM. We designed two separate scenarios for model training. In the first scenario, we utilized data up to February, a period characterized by low uncertainty since these data points are fixed. In the second scenario, we incorporated March data as well, which introduces additional uncertainty due to the imputation process. For each model and scenario, hyperparameter tuning was performed using Optuna (Akiba et al., 2019)., a state-of-the-art optimization framework that efficiently explores high-dimensional hyperparameter spaces. Through iterative trial and error, we determined the optimal number of features by ranking the features based on their importance from a prior LightGBM model.
Finally, we generated our predictions for the year 2025 by aggregating the outputs of the individual models within the ensemble. To quantify the uncertainty of our predictions, we applied a bootstrapping approach, which allowed us to compute confidence intervals for the ensemble prediction. The ensemble methodology not only improved overall prediction accuracy, as measured by the mean absolute error (MAE), but also enhanced the robustness of the prediction against model-specific biases.

References 

•	Akiba, T., Sano, S., Yanase, T., Ohta, T., & Koyama, M. (2019). Optuna: A Next-generation Hyperparameter Optimization Framework. Proceedings of the 25th ACM SIGKDD International Conference on Knowledge Discovery & Data Mining, 2623–2631. https://doi.org/10.1145/3292500.3330701
•	Reid, Philip & Hari, Renata & Beaugrand, Gregory & Livingstone, David & Marty, Christoph & Straile, Dietmar & Barichivich, Jonathan & Goberville, Eric & Adrian, Rita & Aono, Yasuyuki & Brown, Ross & Foster, James & Groisman, Pavel & Helaouet, Pierre & Hsu, Huang-Hsiung & Kirby, Richard & Knight, Jeff & Kraberg, Alexandra & Li, Jianping & Zhu, Zaichun. (2015). Global impacts of the 1980s regime shift. Global Change Biology. 22. 10.1111/gcb.13106. 



# Cherry Blossom Peak Bloom Prediction

This is the official template repository for George Mason’s Department of Statistics cherry blossom peak bloom prediction competition.

This repository contains cleaned and ready-to-use data on peak bloom dates in the *data/* folder, alongside a demo prediction analysis report (*demo_analysis.qmd*).
The demo analysis demonstrates how to load the provided data sets, plot the observed time series, and uses a very simple linear regression model to predict the peak bloom dates for the next year as well as estimate prediction intervals.
The demo analysis requires a [working installation of R](https://cran.r-project.org) and (version ≥ 4.3 strongly suggested), an [installation of quarto](https://www.quarto.org) (e.g., as part of the RStudio IDE), as well as the `tidyverse` suite of packages.

The rendered demo analysis is available at https://competition.statistics.gmu.edu/demo_analysis.html.

## Getting started

To start competing, you need to download the contents of this repository to your computer.
You can do so by either

a. forking this repository to your GitHub account,
b. downloading the ZIP folder

![](figures/readme/download_zip.png)

c. cloning the repository to your local computer.

If you choose options b. or c., you need to set up another publicly accessible GitHub repository (or on another hosting provider like GitLab, Bitbucket, etc.).
To submit your entry for the competition, all your code and data must be accessible in a public Git repository!

Below we provide the steps for forking this repository to your GitHub account and cloning the forked repository to your local computer.

### Prerequisites

Before you fork or clone the repository, you would need to set up Git on your system.
There are many excellent tutorials available online on how to set up Git.
The GitHub specific instructions can be found at https://docs.github.com/en/get-started/quickstart/set-up-git.

For forking, you would also need to sign up for a GitHub account.

### Forking the repository

To fork this repository, locate the _Fork_ button at the top right of the page:

![Fork button at the top-right of the repository](figures/readme/fork_btn.png)

This will copy the repository to your GitHub account under the name _peak-bloom-prediction_.

Next you need to clone the repository to your local computer.
Navigate to **your fork** of the repository on github.com.
The steps are the same as outlined below for cloning the repository, **but the location of the respository will be different**.

More detailed instructions on how to fork a repository can be found under https://docs.github.com/en/get-started/quickstart/fork-a-repo.

### Cloning the repository

Whether you choose to clone this read-only repository or the forked repository under your account, you can follow these instructions to clone the repository to your local computer.

1. Above the file list of the repository on GitHub.com, locate the _Code_ button:

![Clone button at the top of the file list](figures/readme/code_btn.png)

2. This will open a small dialog with the URLs to clone the repository.
   Copy the URL to the Git command line interface or your favorite Git client.

![Clone dialog with URLs for cloning](figures/readme/clone_box.png)

3. If you use a Git client, follow it's instructions on how to clone a remote repository.
   If you use the Git command line interface, open a terminal or command line window.
4. Navigate to the folder/location where you want the cloned repository.
5. Use the `git clone` command in combination with the URL from step 2.
   If you use the original repository (not a fork), you would use the following command:

```sh
$ git clone https://github.com/GMU-CherryBlossomCompetition/peak-bloom-prediction.git
```

6. Press **Enter**.
   You will see something like
```sh
#> Cloning into 'peak-bloom-prediction'...
#> remote: Enumerating objects: 10, done.
#> remote: Counting objects: 100% (10/10), done.
#> remote: Compressing objects: 100% (8/8), done.
#> remote: Total 10 (delta 0), reused 10 (delta 0), pack-reused 0
#> Receiving objects: 100% (10/10), 10.00 KiB | 5.00 MiB/s, done.
```

Now you have the repository cloned to your local computer and you can start coding away!

*Note:* this GitHub repository is read-only and if you clone it to your local computer you can make changes only on your local computer.
You will not be able to *push* your changes to this GitHub repository.
To enter the competition, you must make your repository publicly accessible!

## Competition rules

To enter the competition you must submit your predictions and the URL pointing to your repository via https://competition.statistics.gmu.edu.

**Entries must be submitted by the end of February 28, 2025 (anywhere on earth)**.
If it's February anywhere on earth, your submission will be considered.

The predictions are judged based on the sum of the absolute differences between your predicted peak bloom dates and the publicly posted peak bloom dates:

```
| predicted_bloom_date_kyoto_2025 - actual_bloom_date_kyoto_2025 | +
  | predicted_bloom_date_washingtondc_2025 - actual_bloom_date_washingtondc_2025 | +
  | predicted_bloom_date_liestal_2025 - actual_bloom_date_liestal_2025 | +
  | predicted_bloom_date_vancouver_2025 - actual_bloom_date_vancouver_2025 | +
  | predicted_bloom_date_newyorkcity_2025 - actual_bloom_date_newyorkcity_2025 |
```

The prediction intervals are evaluated based on how many out of the five intervals cover the actual bloom date.
In the case of ties, the sum of the squared lengths of the intervals is used to break the ties.

The true bloom dates for 2025 are taken to be the dates reported by the following agencies/institutions:

- **Kyoto (Japan):** a local news paper from Arashiyama (See http://atmenv.envi.osakafu-u.ac.jp/aono/kyophenotemp4),
- **Washington, D.C. (USA):** National Park Service,
- **Liestal-Weideli (Switzerland):** MeteoSwiss,
- **Vancouver, BC (Canada):** Vancouver Cherry Blossom Festival in collaboration with Douglas Justice, Associate Director, Curator of Collections, UBC Botanical Garden.
- **New York City, NY (USA):** The Washington Square Park Eco Projects in collaboration with the Nature Lab.

The full competition rules are available under https://competition.statistics.gmu.edu.

## License

![CC-BYNCSA-4](https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png)

Unless otherwise noted, the content in this repository is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-nc-sa/4.0/).

For the data sets in the _data/_ folder, please see [_data/README.md_](data/README.md) for the applicable copyrights and licenses.
