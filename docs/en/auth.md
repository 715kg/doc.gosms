---
title: Authentication
icon: material/shield-lock
---

Access to the API is done using a JWT token. You can obtain the token inside the GoSMS control panel in the [API Integration](https://cms.gosms.ru/api) section. The token must be passed in the header of each request in the following format:

Authorization: Bearer $GOSMS_TOKEN

## API Sample Format

The examples in this documentation are described using curl, a command-line HTTP client. Curl is usually installed by default on Linux and macOS computers, and it is available for download on all popular platforms, including Windows.

!!! example "Examples"

    === "Curl"

        ```curl
        bash  curl -X POST     
            -H "Content-Type: application/json"     
            -H "Authorization: Bearer $GOSMS_TOKEN"     
            -d '{"message":"Test message sms","phone_number":"79999999999"}' "https://api.gosms.ru/v1/sms/send"
        ```

    === "Python"

        ```py linenums="1"
        import requests
        import json
        from typing import Dict, Any

        def send_sms(message: str, phone_number: str, token: str) -> str:
            """
            Sends an SMS message using the GoSMS API.

            Parameters:
            - message (str): The content of the SMS message to be sent.
            - phone_number (str): The recipient's phone number.
            - token (str): The authorization token for the GoSMS API.

            Returns:
            - str: The response text from the API call.
            """
            url = "https://api.gosms.ru/v1/sms/send"
            payload = json.dumps({
                "message": message,
                "phone_number": phone_number
            })
            headers = {
                'Content-Type': 'application/json',
                'Authorization': f'Bearer {token}'
            }

            response = requests.post(url, headers=headers, data=payload)
            return response.text

        if __name__ == "__main__":
            message = "Test message sms"
            phone_number = "79999999999"
            token = "GOSMS_TOKEN"

            response_text = send_sms(message, phone_number, token)
            print(response_text)
        ```

    === "PHP"

        ```php linenums="1"
        <?php
        // Create a new HTTP client instance
        $client = new http\Client;

        // Create a new HTTP request instance
        $request = new http\Client\Request;

        // Set the request URL and method
        $request->setRequestUrl('https://api.gosms.ru/v1/sms/send');
        $request->setRequestMethod('POST');

        // Create and append the request body with JSON data
        $body = new http\Message\Body;
        $body->append(json_encode([
            "message" => "Test message sms",
            "phone_number" => "79999999999"
        ]));
        $request->setBody($body);

        // Set the request headers, including Content-Type and Authorization
        $request->setHeaders([
            'Content-Type' => 'application/json',
            'Authorization' => 'Bearer GOSMS_TOKEN'
        ]);

        // Send the request
        $client->enqueue($request)->send();

        // Get the response and output the response body
        $response = $client->getResponse();
        echo $response->getBody();
        ```

    === "Rust"

        ```rust linenums="1"
        use reqwest::blocking::Client;
        use serde_json::{json, Value};
        use std::error::Error;

        fn main() -> Result<(), Box<dyn Error>> {
            // Define the API endpoint and request method
            let url = "https://api.gosms.ru/v1/sms/send";
            let method = "POST";

            // Create the payload with the message and phone number
            let payload = json!({
                "message": "Test message sms",
                "phone_number": "79999999999"
            });

            // Initialize the HTTP client
            let client = Client::new();

            // Create a new HTTP request with the defined method, URL, and payload
            let mut req = client.request(method, url);
            req = req.json(&payload);
            req = req.header("Content-Type", "application/json");
            req = req.header("Authorization", "Bearer GOSMS_TOKEN");

            // Send the request and get the response
            let res = req.send()?;

            // Read the response body
            let body = res.text()?;

            // Print the response body
            println!("{}", body);

            Ok(())
        }
        ```


    === "Golang"

        ```go linenums="1"
        package main

        import (
            "fmt"
            "strings"
            "net/http"
            "io/ioutil"
        )

        func main() {
            // Define the API endpoint and request method
            url := "https://api.gosms.ru/v1/sms/send"
            method := "POST"

            // Create the payload with the message and phone number
            payload := strings.NewReader(`{
                "message": "Test message sms",
                "phone_number": "79999999999"
            }`)

            // Initialize the HTTP client
            client := &http.Client{}

            // Create a new HTTP request with the defined method, URL, and payload
            req, err := http.NewRequest(method, url, payload)
            if err != nil {
                fmt.Println("Error creating request:", err)
                return
            }

            // Add necessary headers to the request
            req.Header.Add("Content-Type", "application/json")
            req.Header.Add("Authorization", "Bearer GOSMS_TOKEN")

            // Send the request and get the response
            res, err := client.Do(req)
            if err != nil {
                fmt.Println("Error sending request:", err)
                return
            }
            defer res.Body.Close()

            // Read the response body
            body, err := ioutil.ReadAll(res.Body)
            if err != nil {
                fmt.Println("Error reading response:", err)
                return
            }

            // Print the response body
            fmt.Println(string(body))
        }
        ```

    === "Js"

        ```js linenums="1"
        const axios = require('axios');

        let data = JSON.stringify({
        "message": "Test message sms",
        "phone_number": "79999999999"
        });

        let config = {
        method: 'post',
        maxBodyLength: Infinity,
        url: 'https://api.gosms.ru/v1/sms/send',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer GOSMS_TOKEN'
        },
        data : data
        };

        axios.request(config)
        .then((response) => {
            console.log(JSON.stringify(response.data));
        })
        .catch((error) => {
            console.log(error);
        });
        ```


    