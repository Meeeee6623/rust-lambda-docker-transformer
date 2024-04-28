# Rust Lambda Sequence Classification

This project is a Rust application that uses the `rust-bert` library for sequence classification and AWS Lambda for deployment.

## Sequence Classification with rust-bert

The `rust-bert` library is a Rust native ready-to-use NLP library, inspired by Hugging Face's Transformers. In this project, we use the `SequenceClassificationModel` from `rust-bert` for sequence classification tasks.

The `SequenceClassificationModel` is initialized with a default configuration (`SequenceClassificationConfig::default()`) in the `my_handler` function. The model then takes an input text from the event and predicts the classification of the sequence.

```rust
let config = SequenceClassificationConfig::default();
let model = SequenceClassificationModel::new(config)?;

let input_text = event["text"].as_str().unwrap_or("");
let output = model.predict(&[input_text.to_string()]);
```

## AWS Lambda Deployment

The application is designed to be deployed on AWS Lambda. The `lambda_runtime` crate is used to provide a runtime for running the application on AWS Lambda.

The `my_handler` function is registered as the handler function for the AWS Lambda runtime. This function is invoked whenever the Lambda function is triggered.

```rust
lambda_runtime::run(handler_fn(my_handler)).await?;
```

## Logging

The application uses the `simple_logger` crate for logging. The log level is set to `Info`.

```rust
SimpleLogger::new().with_level(LevelFilter::Info).init().unwrap();
```

## Running the Application

To deploy the application, you need to have Rust and the Cargo Lambda crate installed. You can then use the following command to run the application:

```bash
cargo lambda deploy
```

Please note that you need to set up your AWS credentials and region in your environment variables to be able to run the application on AWS Lambda.