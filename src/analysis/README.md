# Analysis Scripts / Notebooks

This folder contains code relevant to conducting analysis for Data Provenance Initiative projects.

## Data & Annotations

- `pretrain_data` --- Raw data on C4, RefinedWeb, and Dolma, their URLS and their token counts.
- `agents_counter` --- Counts for various agents.
- `multimodal_terms_data` --- Annotations for the terms of use attached to multimodal data collections.
- `speech_supporting_data` --- Extra metadata for speech datasets.

## Analysis Notebooks

- `text_ft_plots.ipynb` --- Notebook to produce plots for [Data Provenance Initiative first paper](https://arxiv.org/pdf/2310.16787) on text finetuning dataset analysis.
- `robots_analysis.ipynb` --- Notebook to analyze the robots.txt and Terms of Service trends over time.
- `robots_analysis-tables-confusion-matrices-will.ipynb` --- Notebook to generate the [Consent in Crisis](https://www.dataprovenance.org/Consent_in_Crisis.pdf) papers' table comparing website features between the head and random distributions of the web, as well as robots.txt vs terms of service confusion matrices.
- `market_analysis.ipynb` --- Notebook to create plots for WildChat vs website purpose plots, used in the Consent in Crisis paper.
- `multimodal_analysis.ipynb` --- Notebook to compare text, video, and speech datasets.
- `paywall_domain_analysis.ipynb` --- Notebook to analyze the types of domains found behind paywalls.
- `prompt_analysis.ipynb` --- Notebook for plotting WildChat vs content domain type.
- `corpus_robots_trends.ipynb` --- Plotting robots and TOS domain specific trends.

## How to Run Notebooks

Download the folders listed below from the following GDrive: [Organized Raw Data](https://drive.google.com/drive/folders/1jfDAb0qKWZxMhGbCd4o1OIAscE3nc7tv?usp=share_link) and add them your local DPI repo in `src/analysis/data`.

- `domain_estimates` --- Domain estimate sheets for plotting in `corpus_robots_trends.ipynb`
- `GPT_analysis_results` --- GPT responses and grades for TOS policies.
- `raw_annotations` --- Raw annotation files required for plotting results in Consent in Crisis.
- `robots` --- Historical robots policies for the head and 10k random samples.

NOTE: `robots_analysis_p2.ipynb` --- Exploratory data analysis notebook for robots restrictions. None of the results / figures in this notebook were used in the final paper since the data was outdated. Thus, this notebook cannot be fully run but is included for completeness. Run `robots_analysis.ipynb` to reproduce results from the Consent in Crisis paper.

## Aggregated data json

The data has been aggregated into the below json format to streamline future use. `aggregated_data.json` can be download directly from [Organized Raw Data](https://drive.google.com/drive/folders/1jfDAb0qKWZxMhGbCd4o1OIAscE3nc7tv?usp=share_link). 

JSON format:

```json
{
    "<website_url>": {
        "corpora": [
            {
                "corpus": "Dolma",
                "rank": 111
            },
            {
                "corpus": "c4",
                "rank": 92
            }
        ],
        "purpose": [
            "news",
            "..."
        ],
        "modalities": [
            "text",
            "images",
            "..."
        ],
        "paywall": "No",
        "advertisements": true,
        "robots.txt restrictions": {
            "GPTBot": {
                "2016": "No robots",
                "2017": "Partial restricted",
                "...": "<status>"
            },
            "CCBot": {
                "...": "<status>"
            }
        },
        "Terms of Service": {
            "2016": "No AI",
            "...": "<restrictions>"
        }
    }
}
```

To rerun the aggregated json from scratch, you will need the following files from [Organized Raw Data](https://drive.google.com/drive/folders/1jfDAb0qKWZxMhGbCd4o1OIAscE3nc7tv?usp=share_link)— add them your local DPI repo in `src/analysis/data`. Use `analysis/aggregate.py` to regenerate the json if you have all the files below in place.

- `all_pretraining_annos.xlsx` --- These are consolidated pretraining annotations for the ~6k human annotated domains.
- `url_domain_mappings.csv` --- URL to domain mapping CSV. If you need to regenerate it (i.e., updates to the data), you can do so by running `market_analysis.ipynb` and setting the global variable `SAVE_DOMAINS` to True.
- `agent_robots_statistics.json` --- If you need to regenerate it (i.e., updates to the data), you can do so by running `robots_analysis.ipynb` and setting the global variable `SAVE_DATA` to True.
- `agent_tos_statistics.json` --- If you need to regenerate it (i.e., updates to the data), you can do so by running `robots_analysis.ipynb` and setting the global variable `SAVE_DATA` to True.

