# Lab 10: Knowledge check

**Take the screenshot for question 1, and answer question 2 below it, in your own words, in one to three sentences.** Replace the `...` below **Your answer:** with your text.

## 1. From the URL to the function

A classmate calls `${API}books/pg74.txt` and gets an error. To help, you need to know which Lambda function answered the request. In the **AWS Console**, open **API Gateway** → **APIs** → `book-analyzer` → **Resources**, click the `GET` method under `/books/{key}`, and look at its **Integration request**: the setting that tells API Gateway where to pass the request.

Take a screenshot that shows the integration request and the Lambda function it names, and save it as `results/api-gateway.png`.

## 2. Which Lambda function answers the request?

Name the Lambda function from your screenshot. Why did Chalice create this function instead of using `book-analyzer-dev-analyze_new_book` from Lab 07?

**Your answer:**

The function is `book-analyzer-dev`. Chalice creates a separate Lambda function for each event-source decorator like `@app.on_s3_event`, and the Lab 07 function's entry point is `analyze_new_book(event)`, which expects an S3 event and can only be invoked by S3. All the `@app.route` handlers share one function, `book-analyzer-dev`, whose handler is the Chalice `app.app` object that routes the HTTP request from API Gateway to `get_book(key)` and returns the HTTP response.