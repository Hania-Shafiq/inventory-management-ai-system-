# Inventory Management AI System

AI-powered n8n workflow with two core capabilities: an AI chatbot that 
handles customer orders end-to-end, and a scheduled automation that 
monitors stock levels and auto-restocks with WhatsApp alerts.

## Features

### 🤖 AI Customer Support Chatbot
- Understands both English and Urdu (replies in the customer's language)
- Checks product availability from live inventory
- Collects order details (product, quantity, name, address) one at a time
- Validates quantity (rejects 0, negative, or decimal values)
- Validates delivery address (city + house/street/block details required)
- Confirms order only after checking stock — updates inventory & logs order
- Blocks customers from modifying inventory directly

### 📦 Automated Restock System
- Scheduled trigger runs every 24 hours
- Checks all items where Quantity in Stock ≤ Reorder Level
- Auto-updates stock (adds Reorder Quantity)
- Logs the restock in an "Inventory Logs" sheet
- Sends a WhatsApp alert to the store manager with old/new stock details

## Architecture
<img width="1916" height="879" alt="Screenshot 2026-09-07 000552" src="https://github.com/user-attachments/assets/ad172715-ebe2-4ad0-ac98-062245a4991b" />


## Tech Stack
- **n8n** — workflow automation
- **Google Gemini** — AI Agent's language model
- **Google Sheets API** — inventory, orders & logs database
- **WhatsApp Business API (Meta)** — manager alerts

## How It Works

**Chatbot flow:**
1. Customer sends a message via chat
2. AI Agent checks stock via "Get row(s) in sheet"
3. Collects order details step-by-step, validates quantity & address
4. On confirmation → updates stock, logs order, replies with order summary
<img width="1025" height="668" alt="Screenshot 2026-09-07 000356" src="https://github.com/user-attachments/assets/0a6cd093-71ca-4f9e-9a32-55c6e66a0a44" />
<img width="1101" height="857" alt="Screenshot 2026-09-07 000501" src="https://github.com/user-attachments/assets/a2ea9584-ed90-4b92-ae0c-410601423118" />


**Auto-restock flow:**
1. Schedule Trigger fires every 24 hours
2. Reads all rows from the Inventory sheet
3. IF node checks: Quantity in Stock ≤ Reorder Level
4. If true → updates stock, logs the restock, sends WhatsApp alert
<img width="964" height="870" alt="Screenshot 2026-09-07 000630" src="https://github.com/user-attachments/assets/90e32fa7-08b7-49e1-b0e2-adeed0a9921d" />

## Setup
1. Import `workflow.json` into your n8n instance
2. Connect your own Google Sheets, Gemini, and WhatsApp Business credentials
3. Replace placeholder IDs (Sheet ID, Phone Number ID) with your own
