# Twitter DM to Airtable Automation (n8n) 📥

This project automates the collection of Twitter direct messages (DMs) and logs them into **Airtable** with enriched metadata, built using **n8n (self-hosted)**. It streamlines data processing and storage for efficient Twitter DM management.

## ✨ Features

- **Webhook Endpoint**: Securely receives Twitter DM data via POST requests.
- **Metadata Enrichment**: Captures and processes:
  - ✅ Sender
  - ✅ Message content
  - ✅ Formatted timestamp
  - ✅ Message length
  - ✅ Day of the week
  - ✅ Sentiment analysis (placeholder)
  - ✅ Message summary (placeholder)
- **Airtable Integration**: Seamlessly pushes data to Airtable with typecasting.
- **Scalable Design**: Ready for future enhancements like OpenAI-powered sentiment analysis or summarization.

## 🛠️ Tech Stack

- **[n8n](https://n8n.io/)**: Open-source workflow automation platform.
- **[Airtable](https://airtable.com/)**: Cloud-based database for structured data.
- **JavaScript (Function Node)**: Custom logic for data transformation.
- **[Postman](https://www.postman.com/)**: API testing for webhook validation.

## 📋 Requirements

- **n8n**: Self-hosted instance (version 0.200.0 or later recommended).
- **Airtable Account**: Access to a base with a configured table.
- **Airtable PAT**: Personal Access Token for API authentication.
- **Postman (Optional)**: For testing webhook endpoints.
- **Twitter API (Optional)**: For live DM integration.

## 📸 Screenshots

> <img width="1318" height="578" alt="image" src="https://github.com/user-attachments/assets/9faca4f2-db13-4bf4-9944-d6237c3f340d" />
> <img width="1879" height="517" alt="image" src="https://github.com/user-attachments/assets/88948997-e519-4297-aea4-8ec8322914df" />
><img width="988" height="603" alt="image" src="https://github.com/user-attachments/assets/935a90b9-20c8-4980-a541-708896808c2c" />


## 🔄 Workflow Breakdown

### 1. Webhook Node 📡
- **Function**: Receives `POST` requests with Twitter DM data (e.g., from Twitter API or Postman).
- **Setup**: Configured to parse JSON payloads securely.

### 2. Function Node 🧮
- **Function**: Enriches incoming data with metadata.
- **Code**:
  ```javascript
  return items.map(item => {
    const input = item.json;
    const date = new Date(input.Timestamp);

    return {
      json: {
        Sender: input.Sender,
        Message: input.Message,
        Timestamp: date.toISOString(),
        MessageLength: input.Message.length,
        DayOfWeek: date.toLocaleDateString('en-US', { weekday: 'long' }),
        SentimentAnalysis: 'Neutral', // Placeholder
        Summary: 'Summary placeholder' // Placeholder
      }
    };
  });
  ```

### 3. Airtable Node (v2) 📤
- **Function**: Writes enriched data to an Airtable base.
- **Configuration**:
  - Requires **Base ID** and **Table ID**.
  - Uses `typecast: true` for data compatibility.
  - Secured with an **Airtable Personal Access Token (PAT)**.

## 🔒 Security Notes

- **Airtable PAT**: Store your token securely (e.g., in n8n credentials, not in the repo).
- **Base Access**: Configure shared access via [Airtable Account](https://airtable.com/account) for collaboration.
- **Webhook Security**: Ensure your webhook endpoint is protected against unauthorized access.

## 🚀 How to Run

1. **Clone or Import**:
   - Clone this repository or import the `.json` workflow file into n8n.
2. **Configure Airtable**:
   - Update the workflow with your **Airtable Base ID**, **Table ID**, and **PAT**.
3. **Test the Webhook**:
   - Use Postman to send test `POST` requests or connect to a Twitter API bot for live DMs.
4. **Activate Workflow**:
   - Enable the workflow in n8n and verify data in Airtable.
5. **Success**! 🎉 Your Twitter DMs are now logged with metadata.

## 📬 Connect with Me

- **Fiverr**: [Hire me for automation projects](https://www.fiverr.com/sellers/nitrola/edit)
- **LinkedIn**: [Ahmad Raza](https://www.linkedin.com/in/ahmad-raza-403bbd0278)

## 🏷️ Tags

`#n8n` `#automation` `#airtable` `#twitter` `#nocode` `#workflowautomation` `#integration` `#javascript` `#portfolio`

## 📝 License

This project is licensed under the [MIT License](LICENSE).

---

*Built with 💻 by [Ahmad Raza](https://www.linkedin.com/in/ahmad-raza-403bbd0278). Contributions, issues, and feedback are welcome!*
