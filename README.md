# 💵 USD Exchange Rate Alert with n8n

Automation developed with **n8n** to automatically check the current US dollar exchange rate against the Brazilian real, analyze the value, and perform different actions based on the detected exchange rate.

The project uses a public exchange rate API, Google Sheets, and Gmail.

---

## 🚀 What does this automation do?

The workflow works as follows:

1. Receives a request through a Webhook.
2. Retrieves the current USD exchange rate.
3. Converts the value returned by the API.
4. Analyzes the exchange rate using a Switch node.
5. Depending on the value:
   - records the exchange rate in a spreadsheet;
   - or sends an email alert.

Workflow overview:

Webhook  
↓  
HTTP Request  
↓  
USD/BRL Exchange Rate  
↓  
Value Conversion  
↓  
Switch  
├── High exchange rate → Google Sheets  
└── Low exchange rate → Gmail  

---

## 🛠 Technologies Used

- n8n
- REST API
- HTTP Request
- Webhook
- Google Sheets
- Gmail
- JSON
- AwesomeAPI
- Git
- GitHub

---

## 📊 API Used

The automation uses **AwesomeAPI** to retrieve the USD/BRL exchange rate.

Endpoint:

https://economia.awesomeapi.com.br/json/last/USD-BRL

The API returns the current US dollar exchange rate data.

The workflow uses the `bid` field returned by the API and converts it into a numeric value that can be analyzed by n8n.

---

## 🧠 Automation Rules

After retrieving the data from the API, the workflow creates the field:

`valor_convertido`

This value is sent to a **Switch** node.

Currently, two rules are configured.

### 🔴 Exchange rate above R$ 5.30

Condition:

`valor_convertido > 5.30`

The exchange rate is sent to the workflow path identified as:

`nao comprar`

In this path, the value is recorded in Google Sheets.

### 🟢 Exchange rate lower than or equal to R$ 5.22

Condition:

`valor_convertido <= 5.22`

The exchange rate is sent to:

`comprar muito`

In this case, the user receives an email alert informing them that the US dollar exchange rate is low.

---

## 📁 Project Structure

n8n-alerta-dolar/  
├── alerta-dolar.json  
└── README.md  

The main project file is:

`alerta-dolar.json`

It contains the entire n8n workflow structure.

---

## 📥 How to Install

### 1. Download the Project

You can download the project from GitHub using:

`Code → Download ZIP`

Or clone it using Git:

`git clone https://github.com/emanuelvitorfn7-gif/n8n-alerta-dolar.git`

Then enter the project folder:

`cd n8n-alerta-dolar`

---

## 2. Open n8n

You need to have an n8n installation available.

For a local installation, n8n can usually be accessed at:

`http://localhost:5678`

You can also use n8n Cloud.

---

## 3. Import the Workflow

Inside n8n:

1. Open the workflows section.
2. Click the workflow menu.
3. Select the option to import a file.
4. Choose:

`alerta-dolar.json`

The workflow will be loaded into your n8n instance.

---

## 🔑 Configure Your Credentials

Personal credentials should never be shared through GitHub.

Anyone who imports this project must configure their own accounts.

---

## 📈 Google Sheets

Open the node:

`salva a cotaçao na planilha`

Connect your Google account and select your own spreadsheet.

The spreadsheet can contain two columns:

| date | exchange_rate |
|------|---------------|
| 2026/10/04 18:30 | 5.21 |

Then select the desired spreadsheet and sheet inside the Google Sheets node.

---

## 📧 Gmail

Open the node:

`Send an Email`

Connect your own Gmail account.

Then configure the email address that will receive the alerts.

You can also customize:

- recipient;
- subject;
- content;
- alert message.

Example message:

**Subject:** USD Exchange Rate

**Message:**

The US dollar exchange rate is low.

Current exchange rate: R$ 5.21

---

## 🌐 Webhook

The workflow starts through a Webhook.

Method:

`POST`

Configured path:

`nova_transaçao`

After activating the workflow, n8n will provide a production URL.

In a local installation, it may look similar to:

`http://localhost:5678/webhook/nova_transaçao`

You can send a POST request to start the workflow.

PowerShell example:

`Invoke-WebRequest -Method POST -Uri "http://localhost:5678/webhook/nova_transaçao"`

You can also use:

- Postman
- Insomnia
- curl
- another system
- another automation

---

## ▶️ How to Run

After configuring Gmail and Google Sheets:

1. Import the workflow.
2. Configure your credentials.
3. Select your own spreadsheet.
4. Configure the destination email address.
5. Activate the workflow.
6. Copy the production Webhook URL.
7. Send a POST request.
8. n8n will retrieve the current exchange rate.
9. The value will be analyzed.
10. The workflow will execute the corresponding action.

Expected workflow:

Webhook  
↓  
HTTP Request  
↓  
USD to BRL Conversion  
↓  
Switch  
↓  
Decision  
├── Google Sheets  
└── Gmail  

---

## 🔧 Customizing the Values

You can change the values used to determine when each action should be executed.

Open the node:

`cotaçao do dolar`

Then change the conditions.

For example:

Buy:

`<= 5.00`

Do not buy:

`> 5.50`

This allows each user to customize the automation according to their own project goals.

---

## 🔄 Other Currencies

The project can also be adapted to retrieve other currency pairs.

Examples:

- EUR-BRL
- BTC-BRL
- USD-B
