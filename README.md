# openai-api-rs

A Rust crate that provides a simple function for interacting with the OpenAI API and performing language-based tasks. This crate focuses on streaming responses from the API, enabling real-time processing of large amounts of data.

## Features

- Stream-based API: The crate supports streaming responses from the OpenAI API, allowing you to process data in real-time as it becomes available.
- GptStream: The `GptStream` struct provides a convenient interface for interacting with the OpenAI chat completions endpoint.
- JSON Parsing: The crate includes robust JSON parsing capabilities for handling API responses.
- Configuration Options: You can easily configure various parameters such as model selection, temperature, top-p, and more.

## Usage

To use this crate, simply create an instance of the `OpenAIStream` struct, passing your API key as a parameter. Then, call the `gpt_stream` method with your desired input and await the response. The returned `GptStream` object allows you to asynchronously iterate over the streaming API response.

Example:

```rust
use openai_api_rs::{OpenAIStream, GptStream};
use futures::stream::StreamExt;

#[tokio::main]
async fn main() {
    let api_key = "your_api_key";
    let openai_stream = OpenAIStream::new(api_key.to_string());

    let input = r#"
        {
            "model": "gpt-3.5-turbo",
            "messages": [
                {
                    "role": "user",
                    "content": "Write a simple advanced usage of Rust in one sentence"
                }
            ]
        }
    "#;

    let gpt_stream = openai_stream.gpt_stream(input).await.unwrap();
    let mut gpt_stream = Box::pin(gpt_stream);

    while let Some(response) = gpt_stream.next().await {
        println!("{}", response);
    }
}
```

Note: Replace "your_api_key" with your actual OpenAI API key.

For more details and advanced configuration options, please refer to the crate documentation.

Note: This crate is still in development and may be subject to changes and updates.