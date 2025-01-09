
# Website Content Crawler: A Comprehensive Overview

Website Content Crawler is a powerful [Apify Actor](https://docs.apify.com/platform/actors) designed to perform deep crawls of websites and extract text content from web pages. This tool is especially useful for extracting data from websites such as documentation, knowledge bases, help sites, or blogs. It is tailored for tasks like feeding, fine-tuning, or training large language models (LLMs) like [GPT-4](https://openai.com/product/gpt-4), [ChatGPT](https://openai.com/blog/chatgpt), or [LLaMA](https://ai.facebook.com/blog/large-language-model-llama-meta-ai/).

Website Content Crawler is designed to be simple and easily configurable, enabling users to input a website URL for indexing by AI applications. The results can be retrieved in formats like JSON or CSV, making them directly usable for LLMs, [vector databases](https://blog.apify.com/what-is-a-vector-database/), or ChatGPT.

---

## Why Choose Website Content Crawler?

The Crawler is built using [Crawlee](https://crawlee.dev/), Apify’s open-source library for web scraping and crawling. Its features include:

- Crawling **JavaScript-enabled websites** using headless Firefox or simple static sites via raw HTTP.
- Circumventing **anti-scraping protections** with browser fingerprinting and proxies.
- Saving web content in **plain text**, **Markdown**, or **HTML**.
- Crawling **pages behind logins**.
- Downloading files in formats like PDF, DOCX, and CSV.
- Removing unnecessary elements (e.g., headers, footers, ads, or cookie warnings) for accurate data.
- Handling infinite scroll pages.
- Leveraging sitemaps for URL discovery.
- Scaling efficiently for sites with millions of pages using Apify's infrastructure.
- Integration with tools like **LangChain**, **LlamaIndex**, **Pinecone**, and **Qdrant**.

[Start your free trial with ScraperAPI and Apify today!](https://bit.ly/Scraperapi)

---

## Key Features and Capabilities

### Crawling Capabilities

Website Content Crawler can handle different website complexities and types:

1. **Browser-based Crawling**:
   - Ideal for JavaScript-heavy sites and those with bot protections.
   - Uses headless browsers (e.g., Firefox via Playwright).
   - Recognizes and retries blocked requests.

2. **Raw HTTP Crawling**:
   - High-performance crawling for static websites.
   - Faster and cheaper but may not work for dynamic content.

3. **Adaptive Crawling**:
   - Automatically switches between browser and raw HTTP modes to balance speed and performance.

### Content Extraction and Processing

- **Remove unwanted elements**: Strips out headers, footers, modals, and cookie warnings.
- **HTML Transformations**: Converts HTML content to plain text or Markdown for cleaner data extraction.
- **Content Expansion**: Clicks on expandable elements to ensure full data retrieval on dynamic pages.

### Output Options

Data extracted by the crawler can be saved in formats like:
- **Plain text**
- **Markdown**
- **Full HTML**
- **Screenshots** for debugging purposes

The results also include metadata (e.g., author, language, and publishing date) and are stored in the Apify Dataset for easy API export to JSON, XML, or CSV.

---

## Designed for AI and LLMs

### Applications for AI

- **Training LLMs**: Provide accurate, domain-specific data for model training.
- **Custom Chatbots**: Build customer support chatbots with deep knowledge of specific websites.
- **Content Personalization**: Train AI models to write content that mimics the tone and style of existing material.

### Retrieval-Augmented Generation (RAG)

Feed your website’s content into an AI assistant to:
- Answer questions based on existing content.
- Generate new content using the extracted data.

### Summarization, Proofreading, and Translation

Improve or repurpose existing content at scale by feeding scraped data into ChatGPT for:
- Summarization
- Proofreading
- Translation
- Style changes

---

## Integration with Popular Tools

### LangChain Integration

Website Content Crawler integrates seamlessly with LangChain for creating vector databases or AI-powered query interfaces. Here’s how you can use LangChain with the crawler:

#### Python Example
```python
from langchain.indexes import VectorstoreIndexCreator
from langchain_community.utilities import ApifyWrapper
from langchain_core.document_loaders.base import Document
from langchain_openai import OpenAI
from langchain_openai.embeddings import OpenAIEmbeddings

# Set up API keys
os.environ["OPENAI_API_KEY"] = "Your OpenAI API key"
os.environ["APIFY_API_TOKEN"] = "Your Apify API token"

apify = ApifyWrapper()

# Crawl a website and save results to a LangChain document loader
loader = apify.call_actor(
    actor_id="apify/website-content-crawler",
    run_input={"startUrls": [{"url": "https://example.com"}]},
    dataset_mapping_function=lambda item: Document(
        page_content=item["text"] or "", metadata={"source": item["url"]}
    )
)

# Query the vector database
index = VectorstoreIndexCreator(embedding=OpenAIEmbeddings()).from_loaders([loader])
result = index.query_with_sources("What is example.com?", llm=OpenAI())
print(result["answer"])
```

### Vector Databases (Pinecone, Qdrant)

Export crawled data directly to vector databases like Pinecone or Qdrant for semantic search. Incremental updates ensure only new or changed content is embedded.

---

## How to Use Website Content Crawler

### 1. Crawling

Input your **Start URLs** (e.g., `https://example.com/blog/`). The crawler will recursively navigate through linked pages while excluding undesired URLs based on patterns you define.

### 2. Processing

Clean and format the crawled data using:
- **CSS selectors** to include or exclude specific elements.
- **HTML Transformers** to retain only meaningful content.

### 3. Output

Save data in the format of your choice—plain text, Markdown, or structured JSON—for easy integration with your tools.

---

## Pricing

Website Content Crawler is free to use, with charges based only on Apify platform usage. Costs depend on:
- **Crawler type**: Browser-based crawling is costlier than raw HTTP crawling.
- **Website complexity**: Dynamic pages require more resources.

Estimated costs:
- **$0.50–$5 per 1,000 pages** (browser crawling)
- **$0.20 per 1,000 pages** (raw HTTP crawling)

---

## Example Use Case: Scraping Documentation

Input: `https://example.com/docs`

Output: JSON file with structured content, plain text, and metadata.

```json
{
    "url": "https://example.com/docs/introduction",
    "title": "Introduction to Example Docs",
    "text": "Welcome to the Example Docs. This guide provides...",
    "metadata": {
        "author": "John Doe",
        "datePublished": "2023-01-01"
    }
}
```

---

## Get Started with Website Content Crawler

Whether you're training AI models, building chatbots, or generating personalized content, Website Content Crawler offers an efficient, scalable solution for extracting and processing web content.

[Start your free trial today!](https://bit.ly/Scraperapi)
