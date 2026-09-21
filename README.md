# AI Support Agent

An intelligent customer support assistant built with Amazon Bedrock AgentCore and the Strands SDK.

The agent handles common e-commerce support workflows through one conversational interface, including order tracking, refunds, product and policy questions, loyalty calculations, long-term memory, and live web browsing.

## Features

- Track customer orders through AgentCore Gateway
- Process refunds using Lambda-backed MCP tools
- Answer product and policy questions with a Bedrock Knowledge Base
- Remember customer details and preferences across sessions
- Calculate loyalty discounts with AgentCore Code Interpreter
- Browse live websites with AgentCore Browser
- Deploy the agent to AgentCore Runtime

## Architecture

The project combines several AgentCore capabilities:

- **AgentCore Runtime** for cloud deployment
- **AgentCore Gateway** for tool integration through MCP
- **Amazon Bedrock Knowledge Base** for Retrieval-Augmented Generation
- **AgentCore Memory** for cross-session customer context
- **AgentCore Code Interpreter** for exact loyalty calculations
- **AgentCore Browser** for live web access
- **Strands SDK** for agent orchestration

## Project Structure

```text
.
├── main.py
├── pyproject.toml
├── uv.lock
├── product_catalog.txt
├── reflection.md
├── screenshots/
├── lambda/
│   ├── order_tracker.py
│   └── refund_processor.py
└── .bedrock_agentcore.yaml
```

## Setup

Install dependencies:

```bash
uv sync
```

Configure AWS credentials:

```bash
aws configure
```

Update the configuration values in `main.py`:

```python
GATEWAY_URL = "<gateway-url>"
KB_ID = "<knowledge-base-id>"
REGION = "us-east-1"
MEMORY_ID = "<memory-id>"
```

## Deployment

Configure the AgentCore project:

```bash
agentcore configure --entrypoint main.py --name CustomerSupportAgent
```

Deploy the agent:

```bash
agentcore deploy
```

## Test Scenarios

The deployed agent was tested with the following scenarios:

1. Order tracking
2. Refund processing
3. Knowledge Base retrieval
4. Cross-session memory
5. Loyalty discount calculation
6. Live browser access

Test evidence is included in the `screenshots/` folder.

## Example

```bash
agentcore invoke '{"prompt": "Can you track order ORD-001?", "customer_id": "CUST-123", "session_id": "t1"}'
```

A successful response includes the order status, tracking number, carrier, and estimated delivery date.

## Notes

This project was completed in the Udacity VocLabs environment. Some AWS services required additional IAM permissions during deployment and testing, especially Knowledge Base retrieval and AgentCore Browser access.

Because of VocLabs restrictions, the Knowledge Base was created using the managed option instead of manually provisioning OpenSearch Serverless resources.

## Reflection

See `reflection.md` for a short discussion of implementation decisions, challenges, and production considerations.

## Cleanup

After testing, remove the deployed AgentCore runtime with:

```bash
agentcore destroy
```

Additional AWS resources such as the Gateway, Memory resource, Knowledge Base, S3 bucket, API Gateway, and Lambda functions should also be deleted to avoid unnecessary costs.
