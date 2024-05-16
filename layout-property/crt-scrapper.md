# How to use the CRT Scrapper?

Scraper Library is a versatile tool for scraping data from web pages. It provides various events to customize and control the scraping process, allowing users to retrieve data efficiently and reliably.

## Installation

To install the Scraper Library, use the following command:

```bash
npm i crt-scrapper
```

## Usage 

```javascript
const {
    scrapeData
} = require('crt-scrapper');

const url = 'https://www.trendyol.com/sanaozel/2?versionKey=singleProducts_JFY_Original_Man_Deng';
const targetClass = '.wrapper';

const options = {
    beforeRequest: (url) => {
        console.log(`Sending request to ${url}`);
    },
    afterRequest: (response) => {
        console.log(`Received response with status ${response.status}`);
    },
    onError: (error) => {
        console.error(`An error occurred: ${error.message}`);
    },
    beforeParse: ($) => {
        console.log('Parsing HTML content...');
    },
    afterParse: (data) => {
        console.log(`Scraped data: ${data}`);
    },
    beforeRetry: (error) => {
        console.log(`Retrying due to error: ${error.message}`);
    },
    afterRetry: (error) => {
        console.log('Retry attempt completed.');
    },
    beforeResponse: () => {
        console.log('Processing HTTP response...');
    },
    timeout: 5000,
    headers: {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.212 Safari/537.36',
    },
};

scrapeData(url, targetClass, options)
    .then(result => {
        console.log(result);
    })
    .catch(error => {
        console.error(error);
    });
```

## Events

 1. ### beforeRequest Event
   The `beforeRequest` event is triggered before sending the HTTP request. It provides the URL of the request as a parameter.

<b>Example:</b>

```javascript
beforeRequest: (url) => {
    console.log(`Sending request to ${url}`);
}
```

2. ### afterRequest Event
    The `afterRequest` event is triggered after receiving the HTTP response. It provides the response object as a parameter.

<b>Example:</b>

```javascript
afterRequest: (response) => {
    console.log(`Received response with status ${response.status}`);
}
```

3. ### onError Event
   The `onError` event is triggered when an error occurs during scraping. It provides the error object as a parameter.

<b>Example:</b>

```javascript
onError: (error) => {
    console.error(`An error occurred: ${error.message}`);
}
```

4. ### beforeParse Event
The `beforeParse` event is triggered before parsing the HTML content. It provides the Cheerio instance ($) as a parameter.

<b>Example:</b>

```javascript
beforeParse: ($) => {
    console.log('Parsing HTML content...');
}
```

5. ### afterParse Event
   The `afterParse` event is triggered after parsing the HTML content. It provides the scraped data as a parameter.
   <b>Example:</b>

```javascript
afterParse: (data) => {
    console.log(`Scraped data: ${data}`);
}
```

6. ### beforeRetry Event
   The `beforeRetry` event is triggered before retrying the scraping process due to an error. It provides the error object as a parameter.

      <b>Example:</b>

```javascript
beforeRetry: (error) => {
    console.log(`Retrying due to error: ${error.message}`);
}
```

7. ### afterRetry Event
The `afterRetry` event is triggered after a retry attempt is completed.

      <b>Example:</b>

```javascript
afterRetry: () => {
    console.log('Retry attempt completed.');
}
```

8. ### beforeResponse Event

The `beforeResponse` event is triggered before processing the HTTP response.

      <b>Example:</b>

```javascript
beforeResponse: () => {
    console.log('Processing HTTP response...');
}
```

9. ### XML Output

The `format`option allows you to specify the output format as XML. The scraped data will be returned in XML format.

      <b>Example:</b>

```javascript
const options = {
    format: 'xml',
};
```

10. ### CSV Output
    The `format` option allows you to specify the output format as CSV. The scraped data will be returned in CSV format.

```javascript
const options = {
    format: 'csv',
};
```
