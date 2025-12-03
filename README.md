## Customer Service Agent for Clothing Retailer
### Custom AI Agent with Logging and Session Memory

This project contains code for a custom retail AI agent with a recommendation system. The agent considers past purchases and cross references these with any returns, then recommends items that would suit the customer's tastes. It will look up returns and past purchases. 

The project includes databases for testing purposes, and simplified categorization of items for the recommendation system. 

The agent's functionality includes logging and session memory.


### Architecture and Methodology

The agent's code is contained in the file ai-agent.ipynb.

The agent uses gemini-2.5-flash-lite LLM model for reasoning and planning. The agent has access to 3 tools for answering user prompts: purchase_history, customer_returns, and item_recommendation. The item_recommendation tool recommends up to 6 items. 

### Databases included for Testing

There are 3 databases included for testing

customer_database: This database is dictionary. Each item contains a customer's username and userid.

product_style_database: This database is a list of dictionaries. Each dicationary is a group of items that share at least 2 attributes. Each contains the product name and the associated product's UPC number.

purchase_history_databse: This database is a ditionary. Each item consists of a customer userid and the list of UPC number for items purchased by that customer.

returns_database: Thie database is a dictionary. Each item in the dictionary consists of a customer userid and the list of UPC numbers for items returned by that customer

### Tools

The item_recommendation tool takes in the userid and checks the customer's purchases by calling the get_purchase_history tool. It then calls the get_customer_returns tool and removes any items from the list produced to remove any returne items. It then uses the product_style_database to fetch a list of similar items up to 6.  

#### Memory

The agent uses ADK’s built‑in InMemoryMemoryService to provide session‑scoped memory. This allows the agent to hold context across multiple turns in a single conversation, such as remembering the active user ID (abigail454) or previously discussed preferences. The memory persists only for the duration of the session and is not stored permanently. 
To ensure memory is updated consistently, we define an after_agent_callback (auto_save_to_memory) that automatically saves the session state into memory after each agent turn. 

#### Logging

The agent has an integrated LoggingPlugin in its runner configuration to provide observability. The logging plugin captures standardized traces of inputs, outputs, and tool calls, making it easier to debug, monitor, and audit agent behavior. This allows us to track how recommendations are generated, verify that memory is being updated correctly, and identify any errors or unexpected tool responses.


### Setup
Setup a .env file with your API key. 

To run the agent, run ai-agent.ipynb from the top. 
To run a new prompt, go to the "Test the Agent!" heading at the bottom and change the value of the "prompt" variable. 


## Potential Additions and Fixes

The recommendation tool could include a rating system to rank the recommended items in order of relevance. 

We could also have it call a get_popular_item tool, to return a list of recommended items, in the case that the tool returns "none" (this would occur if the customer has no purchase history.)


![Screenshot_2-12-2025_144728_www zara com](https://github.com/user-attachments/assets/49984d81-fdb7-418b-a577-4bf0bc553da4)



