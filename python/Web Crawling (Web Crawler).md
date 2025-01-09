
# Web Crawling (Web Crawler)

## Introduction

Web crawling is a powerful feature provided by web scraping APIs that enables you to extract content from any website, select the data you need, and batch deliver it to you. With web crawling, you can perform **URL searches, scrape all pages of a website, find all URLs within a domain**, and more.

This tutorial walks you through the workflow of web crawling, demonstrating how to retrieve public data from an e-commerce website.

Web crawlers often use [Basic HTTP Authentication](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication), which requires sending a username and password.

Before using a web crawler, make sure to read the sections on [filters](https://developers.oxylabs.io/cn/pa-chong-api/wang-luo-pa-chong-web-crawler#shai-xuan) and [usage statistics](https://developers.oxylabs.io/cn/pa-chong-api/wang-luo-pa-chong-web-crawler#yong-liang-tong-ji) in the documentation. These sections explain how filters operate and how fees are calculated for this feature.

---

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more. 👉 [Start your free trial today!](https://bit.ly/Scraperapi)

---

If you feel overwhelmed and need assistance, you can contact us via our [official website](https://oxylabs.cn/) through WeChat, QQ, or 24/7 live chat support.

## Endpoints

### Create a New Job

Use this endpoint to initiate a new web crawling job.

**Payload Example**:

```json
{
  "url": "https://example.com",
  "filters": {
    "crawl": [".*"],
    "process": [".*"],
    "max_depth": -1
  },
  "scrape_params": {
    "source": "universal",
    "user_agent_type": "desktop"
  },
  "output": {
    "type_": "sitemap"
  },
  "upload": {
    "storage_type": "s3",
    "storage_url": "http://s3.amazonaws.com/{bucket_name}/"
  },
  "context": {
    "follow_amazon_deals": false
  }
}
```

**Sample Response**:

```json
{
  "id": "10374369707989137859",
  "client": "username",
  "job_params": {
    "url": "https://example.com",
    "filters": {
      "crawl": [".*"],
      "process": [".*"],
      "max_depth": -1
    },
    "scrape_params": {
      "source": "universal",
      "geo_location": null,
      "user_agent_type": "desktop",
      "render": null
    },
    "output": {
      "type": "sitemap",
      "selector": null
    },
    "upload": {
      "storage_type": "s3",
      "storage_url": "http://s3.amazonaws.com/{bucket_name}/"
    },
    "context": {
      "follow_amazon_deals": false
    }
  },
  "_links": [
    {
      "rel": "self",
      "href": "http://ect.oxylabs.io/v1/jobs/10374369707989137859",
      "method": "GET"
    },
    {
      "rel": "stop-indexing",
      "href": "http://ect.oxylabs.io/v1/jobs/10374369707989137859/stop-indexing",
      "method": "POST"
    }
  ],
  "events": [],
  "created_at": "2021-11-19 14:32:01",
  "updated_at": "2021-11-19 14:32:01"
}
```

### Stop a Job

Use this endpoint to stop a specific job.

### Resume a Job

Use this endpoint to resume a paused job.

- **Method**: `POST`  
- **Authentication**: `Basic`

**Sample Response**:

```json
null
```

### Get Job Information

Use this endpoint to fetch details about an existing job.

- **Method**: `GET`  
- **Authentication**: `Basic`

**Sample Response**:

```json
{
  "id": "10374369707989137859",
  "client": "username",
  "job_params": {
    "url": "https://example.com",
    "filters": {
      "crawl": [],
      "process": [],
      "max_depth": -1
    },
    "scrape_params": {
      "source": "universal",
      "geo_location": null,
      "user_agent_type": "desktop",
      "render": null
    },
    "output": {
      "type": "sitemap",
      "selector": null
    },
    "upload": {
      "storage_type": "s3",
      "storage_url": "http://s3.amazonaws.com/{bucket_name}/"
    },
    "context": {
      "follow_amazon_deals": false
    }
  },
  "_links": [
    {
      "rel": "self",
      "href": "http://ect.oxylabs.io/v1/jobs/10374369707989137859",
      "method": "GET"
    }
  ],
  "events": [
    {
      "event": "job_indexing_finished",
      "status": "done",
      "reason": null,
      "created_at": "2021-11-19 14:32:16"
    },
    {
      "event": "job_results_aggregated",
      "status": "done",
      "reason": null,
      "created_at": "2021-11-19 14:32:17"
    }
  ],
  "created_at": "2021-11-19 14:32:01",
  "updated_at": "2021-11-19 14:32:01"
}
```

---

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more. 👉 [Start your free trial today!](https://bit.ly/Scraperapi)

---

### Get Sitemap

Use this endpoint to retrieve the list of URLs discovered during the job.

### Fetch Aggregated Results

Use this endpoint to obtain the results of a job. The results may include:

- A list of URLs (an index).
- An aggregated file containing all parsed results.
- An aggregated file containing all HTML results.

**Endpoint**: `https://ect.oxylabs.io/v1/jobs/{id}/aggregate`  
**Method**: `GET`  
**Authentication**: `Basic`

## Query Parameters

### Scrape Parameters

You can fine-tune your configurations using additional scraper API parameters. The value of most parameters depends on the type of crawler you're using.

#### `geo_location`

Defines the geographic location for the results. The format of the `geo_location` parameter depends on the chosen `source`. Refer to the documentation of your selected source for more details.

#### `render`

Enables JavaScript rendering. Use this when the target requires JavaScript to load content. Set the parameter value to `html` to enable this feature. [Learn more](https://developers.oxylabs.io/cn/pa-chong-api/ru-men/api-can-kao/quan-ju-can-shu-zhi#render).

#### `source`

Specifies the crawler type to use during the job. The parameter value depends on the URL you submit. For example:

| URL                 | Source          |
|---------------------|-----------------|
| Any Google URL      | `google`        |
| Any AliExpress URL  | `aliexpress`    |
| Any other URL       | `universal`     |

### Filters

Filters allow you to control the breadth and depth of your scraping jobs.

#### Regex Examples

| Regex Value                                    | Description                                           |
|------------------------------------------------|-------------------------------------------------------|
| `.*`                                          | Matches any character sequence (except line breaks). |
| `https:\/\/www.amazon.com\/[^\/]*\/[^\/]*`    | Matches URLs on Amazon with a path of up to 2 slashes.|

#### `max_depth`

Defines the maximum URL chain length the web crawler can follow:

| Value  | Description                        |
|--------|------------------------------------|
| `-1`   | No depth limit (default setting).  |
| `0`    | Crawl only the starting page.      |
| `1`    | Crawl all URLs found on the start page.|

---

Optimize your web crawling process with [ScraperAPI](https://bit.ly/Scraperapi), the ultimate solution for handling millions of requests seamlessly.
