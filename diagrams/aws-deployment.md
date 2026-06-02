flowchart TD
    Internet[Internet]
    Twilio[Twilio Webhook]
    EC2[Amazon EC2 - Dockerized FastAPI App]
    Aurora[(Amazon Aurora PostgreSQL)]
    Secrets[AWS Secrets Manager / SSM Parameter Store]
    Logs[Amazon CloudWatch Logs]
    OpenAI[OpenAI API]

    Internet --> Twilio
    Twilio --> EC2
    EC2 --> Aurora
    EC2 --> Secrets
    EC2 --> Logs
    EC2 --> OpenAI
