# Text Summarization and Bias Detection in Indian News

This project presents an end-to-end Natural Language Processing (NLP) pipeline that scrapes political news articles from major Indian media outlets, summarizes them, and analyzes them for sentiment and political bias. The goal is to programmatically gather and analyze media coverage of specific events (in this case, the Delhi and Bihar elections) to uncover potential patterns in reporting across different sources.

## Features

- **Multi-Source Web Scraping**: Gathers news articles from **India Today, NDTV, Times of India (TOI),** and **The Hindu** using `requests`, `BeautifulSoup`, and `selenium`.
- **Abstractive Text Summarization**: Employs the `facebook/bart-large-cnn` and `t5-base` models from Hugging Face Transformers to generate concise summaries of long articles.
- **Sentiment Analysis**: Determines the sentiment (e.g., POSITIVE/NEGATIVE) of each article's summary.
- **Political Bias Detection**: Implements two approaches to classify bias:
    - **Zero-Shot Classification**: Uses the `facebook/bart-large-mnli` model to classify summaries as "pro-government," "anti-government," or "neutral."
    - **Rule-Based Method**: A simpler keyword-based classifier for comparison and robustness.
- **Data Aggregation**: Consolidates all analyzed data into a single, clean CSV file (`merged_election_news_dataset.csv`).
- **Comparative Visualization**: Creates bar charts using `matplotlib` and `seaborn` to compare bias and sentiment distributions across different news sources.

## Workflow

The project follows a systematic pipeline:

1.  **Data Collection**: The notebook contains separate scrapers for each news source. They navigate to the elections section and collect article links and titles based on relevant keywords (e.g., "Delhi election", "Bihar election", "BJP", "AAP").
2.  **Content Extraction**: For each article link, the scraper extracts the full text content from the news page.
3.  **NLP Analysis**: Each article's content is processed through a multi-step NLP pipeline:
    - The text is summarized to capture the core message.
    - The sentiment of the summary is analyzed.
    - The political bias of the summary is classified.
4.  **Data Storage**: The processed data (title, URL, summary, sentiment, bias, source, etc.) is stored in a `pandas` DataFrame and saved to a source-specific CSV file.
5.  **Aggregation**: All individual CSV files are merged into a final dataset `merged_election_news_dataset.csv` for unified analysis.
6.  **Visualization**: The final dataset is used to generate plots that visualize the findings, offering a comparative look at the media landscape.

## Technologies Used

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=yellow)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)
![Pandas](https://img.shields.io/badge/Pandas-2.x-blue?logo=pandas)
![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97_Hugging_Face-Transformers-yellow)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.x-orange?logo=scikit-learn)
![Selenium](https://img.shields.io/badge/Selenium-4.x-green?logo=selenium)
![BeautifulSoup](https://img.shields.io/badge/BeautifulSoup-4.x-green)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.x-blue?logo=matplotlib)
![Seaborn](https://img.shields.io/badge/Seaborn-0.12-blue?logo=seaborn)

## How to Run

This project is designed to be run in a Jupyter environment like Google Colab, which simplifies dependency management for libraries like `selenium`.

1.  **Clone the Repository**
    ```bash
    git clone https://github.com/Hacxmr/NLP_Project.git
    cd NLP_Project
    ```

2.  **Install Dependencies**
    The notebook installs dependencies in the first few cells. To install them manually, run:
    ```bash
    pip install requests beautifulsoup4 pandas selenium transformers torch matplotlib seaborn scikit-learn
    ```
    *Note: `torch` is a dependency for the `transformers` library.*

3.  **Execute the Notebook**
    - Open `NLP_Project (1).ipynb` in Google Colab or a local Jupyter Notebook instance.
    - Run the cells sequentially. The notebook is structured to:
        - Install packages.
        - Initialize NLP models.
        - Scrape, process, and save data for each news source.
        - Merge the generated CSV files.
        - Create visualizations.

    > **Note on Local Execution**: If running `selenium` locally (not on Colab), you will need to have Google Chrome installed and download the corresponding `chromedriver`. The code in the notebook is pre-configured for a Colab environment and may need slight modifications for a local setup.

## Results & Visualization

The analysis produces visualizations that provide insights into the scraped data.

### Bias Distribution per News Source
This chart shows the count of articles classified with a specific political bias for each media outlet. It helps identify if certain news sources have a tendency to publish more pro-government, anti-government, or neutral content on the topic.

![Bias Distribution Chart](https://i.ibb.co/6P74b7K/bias-distribution.png)


### Sentiment Distribution per State
This chart visualizes the overall sentiment (Positive, Negative, Neutral) of articles related to the Delhi and Bihar elections, allowing for a comparison of the narrative tone for each region.

![Sentiment Distribution Chart](https://i.ibb.co/3cYfG2y/sentiment-distribution.png)


## Limitations and Future Work

- **Scraper Fragility**: The web scrapers are dependent on the current HTML structure of the target websites and may break if the sites are redesigned.
- **Simplistic Bias Detection**: The bias detection models are not fine-tuned for the nuances of the Indian political landscape. The rule-based approach is particularly basic and serves as a baseline.
- **Limited Dataset**: The dataset size is relatively small and focused on specific election events, which may not be representative of the outlets' overall reporting.

### Potential Improvements
- **Fine-tuning Models**: Fine-tune the summarization and bias classification models on a custom-labeled dataset of Indian news for better accuracy and context-awareness.
- **Advanced Bias Metrics**: Implement more sophisticated bias detection techniques, such as analyzing framing, word choice, and story placement.
- **Web Interface**: Develop a simple web application using **Streamlit** or **Flask** to allow users to input a news article URL and see the analysis in real-time.
- **Scalability**: Expand the number of news sources and automate the scraping process to run periodically, building a larger longitudinal dataset.
