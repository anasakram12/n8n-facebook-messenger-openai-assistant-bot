# Facebook Messenger Receptionist Bot with Airtable & OpenAI Assistant API (v2 Threads)

## Overview

This **n8n workflow** automates a **Facebook Messenger Receptionist Bot** that maintains conversational context by leveraging:

* **Facebook Messenger Webhook** for receiving user messages
* **Airtable** as a database to store user-to-thread mappings
* **OpenAI Assistant API (v2 Threads)** for conversational AI with memory
* **Facebook Graph API** for sending replies back to users

The bot creates persistent conversation threads for each user, enabling context-aware replies that improve user experience and engagement.

---

## Features

* **Persistent user conversations** with thread memory stored in OpenAI Assistant API
* Automatic **thread management**: detects existing conversations or creates new threads
* **User-to-thread mapping** stored and managed in Airtable for quick lookups
* **Real-time communication** via Facebook Messenger API
* Seamless integration using **n8n workflow automation**

---

## Workflow Details

### Core Flow:

1. **Facebook Webhook**: Receives incoming messages from users.
2. **Extract Details**: Parses the Facebook payload to extract `senderId` and `messageText`.
3. **Check Thread in Airtable**: Searches if a thread for this user already exists.
4. **Conditional Branch**:

   * If **Thread Exists**: Use existing thread ID.
   * If **Thread Does Not Exist**: Create new OpenAI Assistant Thread and store mapping in Airtable.
5. **Send message to OpenAI Assistant**: Pass user message with thread context to get AI response.
6. **Format AI response** for Facebook Messenger.
7. **Send AI reply** back to user via Facebook Graph API.

---

### Workflow Nodes Summary

| Node Name            | Type                        | Purpose                                                    |
| -------------------- | --------------------------- | ---------------------------------------------------------- |
| Facebook\_Webhook    | Webhook                     | Receives Facebook Messenger POST requests                  |
| Extract\_Details     | Code Node                   | Extracts `senderId` & `messageText` from Facebook payload  |
| Search records       | Airtable Search             | Checks if Thread ID exists for user in Airtable            |
| Check\_ThreadID      | Set Node                    | Sets boolean flag if thread exists                         |
| If                   | IF Node                     | Branch: Existing thread or create new thread               |
| Create OpenAI Thread | HTTP Request (OpenAI API)   | Creates new Assistant Thread                               |
| Get ThreadID         | Set Node                    | Stores new Thread ID and Sender ID                         |
| Create a record      | Airtable Create             | Saves new User & Thread mapping in Airtable                |
| Assistant\_Model     | OpenAI Assistant Node       | Sends user message with thread context to OpenAI Assistant |
| Organize\_Response   | Code Node                   | Formats AI response payload for Facebook Messenger         |
| Send Response        | HTTP Request (Facebook API) | Sends AI reply to user on Messenger                        |
| Sticky Note          | Sticky Note                 | Documentation note (non-executable)                        |

---

## Prerequisites

* **n8n instance** (self-hosted or cloud)
* **Facebook Developer App** with Messenger setup and webhook configured
* **Airtable base and API key**
* **OpenAI API key with Assistant v2 Threads access**
* Basic knowledge of n8n workflows

---

## Setup Instructions

1. **Configure Facebook Developer App:**

   * Create a Facebook App and set up the Messenger product.
   * Set webhook URL to the n8n Webhook node URL.
   * Generate Facebook Page Access Token.

2. **Set up Airtable:**

   * Create a base with a table (e.g., `Call Threads`) to store:

     * User ID (senderId)
     * Thread ID
   * Obtain Airtable API key and base ID.

3. **OpenAI API:**

   * Get OpenAI API key with access to Assistant API v2 Threads.
   * Adjust HTTP Request node URLs and headers accordingly.

4. **Import this n8n workflow:**

   * Import the provided JSON into your n8n instance.
   * Fill in credentials and API keys in the respective nodes.

5. **Test the flow:**

   * Send a message to your Facebook Page.
   * Confirm if the bot responds with context-aware replies.

---

## Use Cases

* Automated receptionists for businesses
* Customer support chatbots with memory
* FAQ bots that maintain conversation context
* Lead qualification and nurturing via Messenger

---

## Visual Flow Diagram

![Workflow Diagram](.workflow_diagram.png)


---

## Contributing

Feel free to contribute by submitting issues or pull requests to improve this workflow.

---

## License

This project is licensed under the MIT License.

---

## Contact

For support or questions, please contact Anas Akram https://www.linkedin.com/in/anas-akram.

---

