# 01. URL Shortener Practice Problem

## Overview

In this lesson, we will explore the design and implementation of a URL shortener service, a common practice problem in technical interviews. A URL shortener takes long URLs and converts them into shorter, more manageable links. This problem tests a candidate's ability to design scalable systems, manage data storage, and implement algorithms efficiently. We will discuss the requirements, design considerations, and potential solutions for building a URL shortener.

## Problem Statement

Design a URL shortener service that provides the following functionalities:

1. **Shortening a URL**: Given a long URL, generate a unique short URL that can redirect to the original URL.
2. **Retrieving the Original URL**: Given a short URL, retrieve the corresponding long URL.
3. **Handling Collisions**: Ensure that the generated short URLs are unique and handle any potential collisions.
4. **Analytics (Optional)**: Track the number of times a short URL has been accessed.

## Requirements

### Functional Requirements

1. **Shorten URL**:

   - Input: A long URL (e.g., `https://www.example.com/some/long/path`)
   - Output: A short URL (e.g., `https://short.ly/abc123`)

2. **Retrieve Original URL**:

   - Input: A short URL (e.g., `https://short.ly/abc123`)
   - Output: The original long URL (e.g., `https://www.example.com/some/long/path`)

3. **Collision Handling**: Ensure that if two different long URLs generate the same short URL, a new unique short URL is created.

4. **Analytics (Optional)**: Count the number of times a short URL has been accessed.

### Non-Functional Requirements

1. **Scalability**: The service should be able to handle a large number of requests efficiently.
2. **Performance**: Shortening and retrieving URLs should be done quickly, with minimal latency.
3. **Data Persistence**: Store the mapping between short URLs and long URLs in a persistent storage solution.

## Design Considerations

### Data Storage

- **Database**: A key-value store (such as Redis or DynamoDB) can be used to store the mapping of short URLs to long URLs. The key would be the short URL, and the value would be the long URL.
- **Indexing**: Use indexing to optimize retrieval speed for long URLs based on short URLs.

### URL Encoding

- **Base Conversion**: Use a base conversion technique to convert a unique identifier (e.g., an incrementing integer) into a short string. This can be done using a custom alphabet (e.g., alphanumeric characters) to generate a unique short URL.
- **Hashing**: Alternatively, apply a hashing algorithm (e.g., MD5 or SHA-256) to the long URL and use a portion of the hash to create a short URL. Ensure that collisions are managed appropriately.

### Collision Handling

- **Check for Existing Short URLs**: Before assigning a short URL, check if it already exists in the database. If it does, generate a new one until a unique short URL is found.
- **Randomized Generation**: Generate short URLs randomly and check for collisions, although this may require additional checks to ensure uniqueness.

### API Design

Design a simple RESTful API with the following endpoints:

1. **POST /shorten**

   - Request Body: `{ "longUrl": "https://www.example.com/some/long/path" }`
   - Response: `{ "shortUrl": "https://short.ly/abc123" }`

2. **GET /{shortUrl}**
   - Request: `GET https://short.ly/abc123`
   - Response: Redirect to the original long URL.

## Implementation

### Example Implementation in Python

Here’s a simplified version of how you might implement a URL shortener service in Python:

```python
import random
import string
from flask import Flask, request, redirect, jsonify

app = Flask(__name__)

# In-memory storage for demonstration purposes
url_mapping = {}
base_url = "https://short.ly/"
short_url_length = 6

def generate_short_url():
    """Generate a random short URL."""
    characters = string.ascii_letters + string.digits
    short_url = ''.join(random.choices(characters, k=short_url_length))
    return base_url + short_url

@app.route('/shorten', methods=['POST'])
def shorten_url():
    long_url = request.json.get('longUrl')
    if not long_url:
        return jsonify({"error": "Invalid URL"}), 400

    # Generate a unique short URL
    short_url = generate_short_url()
    while short_url in url_mapping:
        short_url = generate_short_url()

    # Store the mapping
    url_mapping[short_url] = long_url
    return jsonify({"shortUrl": short_url})

@app.route('/<short_url>', methods=['GET'])
def redirect_to_long_url(short_url):
    long_url = url_mapping.get(base_url + short_url)
    if long_url:
        return redirect(long_url)
    return jsonify({"error": "URL not found"}), 404

if __name__ == '__main__':
    app.run(debug=True)
```

### Explanation of the Implementation

1. **Flask Framework**: The example uses Flask, a lightweight web framework for Python, to create the API.
2. **In-Memory Storage**: For simplicity, an in-memory dictionary (`url_mapping`) is used to store the mapping of short URLs to long URLs.
3. **Short URL Generation**: The `generate_short_url` function creates a random string of characters to form the short URL.
4. **Endpoints**:
   - **POST /shorten**: Accepts a long URL and returns a generated short URL.
   - **GET /{shortUrl}**: Redirects to the original long URL based on the short URL provided.

## Conclusion

The URL shortener practice problem provides an excellent opportunity to demonstrate system design, algorithm implementation, and API development skills. By understanding the requirements, design considerations, and implementation details, candidates can effectively tackle this problem in a technical interview setting. Building a URL shortener service not only tests a candidate's technical abilities but also their understanding of scalability, data management, and user experience.

Next: [02. Distributed Key-Value Store](./02-distributed-key-value-store.md)
