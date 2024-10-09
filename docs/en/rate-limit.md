---
title: Request Rate Limiting
icon: material/speedometer-slow
---

To ensure stability for all users, GoSMS protects its API from spikes in incoming traffic by analyzing the number of requests from each account to each endpoint. If your application sends more than 10 requests per second to a single endpoint, the API may respond with an HTTP status code 429 Too Many Requests.