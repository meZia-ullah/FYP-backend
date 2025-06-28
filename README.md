# 🔧 Backend – Bug Severity Prediction API

This is the **Node.js/Express backend** for the Final Year Project:  
🎓 **"An Automated Approach for the Prediction of the Severity Level of Bug Reports Using LLMs"**

The backend serves as a RESTful API that receives bug report text, processes it, and uses a Machine Learning model (XLNet) to predict the severity level of the bug.

---

## 🎯 Objective

To develop a scalable and modular backend that:
- Accepts bug report input via API
- Sends the text to a Python-based machine learning model
- Returns the predicted severity level and confidence score

---

## 🧰 Technologies Used

| Category             | Tools / Libraries                          |
|----------------------|---------------------------------------------|
| Server Framework     | [Express.js](https://expressjs.com)        |
| Runtime Environment  | [Node.js](https://nodejs.org)              |
| ML Integration       | Python (XLNet / LLM via script or Flask)   |
| Communication        | `child_process` or `axios` (if using Flask)|
| Middleware           | `cors`, `dotenv`, `body-parser`            |

---

## 📦 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/your-username/your-repo-name.git
cd backend
```

### 2. Install dependencies
```bash
npm install
```

### 3. Create `.env` file
```env
PORT=5000
PYTHON_SERVER=http://localhost:8000/predict   # Only if using Flask API
```

> If you're using `child_process` to run a Python script locally instead, you can ignore `PYTHON_SERVER`.

### 4. Start the server
```bash
npm start
```

The server will run at: [http://localhost:5000](http://localhost:5000)

---

## 📡 API Endpoint

### **POST** `/api/predict`

#### Request Body:
```json
{
  "bug_report": "App crashes after clicking the save button."
}
```

#### Sample Response:
```json
{
  "severity": "Major",
  "confidence": 0.88
}
```

---

## 🔄 Python Model Integration

### Option 1: Using `child_process` to run `predict.py`
- Backend calls a local Python script directly.
- Output is read from `stdout` and parsed back into JSON.

```js
const { spawn } = require('child_process');
const python = spawn('python', ['predict.py', reportText]);
```

### Option 2: Using Flask-based Python API
- ML model hosted separately (e.g., `http://localhost:8000/predict`)
- Use `axios` to send POST request to Flask server.

```js
axios.post(process.env.PYTHON_SERVER, { bug_report })
```

---

## 🧪 Python Model (External)

Ensure your model (XLNet or LLM) is:
- Trained and saved (e.g., `model.pkl` or `model.pt`)
- Wrapped in a prediction script or RESTful Flask API
- Returns JSON response like:

```json
{
  "severity": "Critical",
  "confidence": 0.94
}
```


---

## 🔒 Security & Middleware

- `cors` – allows frontend to connect (React on port 3000)
- `body-parser` – parses JSON request body
- `dotenv` – manages environment configs securely

---

## 🔍 Logging & Error Handling

- Basic try-catch error handling on API routes
- Server console logs errors for debugging
- Future scope: integrate Winston or Morgan for logging

---

## 📌 Future Enhancements

- Add input validation and sanitization
- Implement logging and rate limiting
- Deploy model inference on cloud (e.g., Hugging Face, FastAPI on Render)
- Add database for storing prediction history (MongoDB/PostgreSQL)

---

## 👨‍💻 Authors

- **Zia Ullah** – Python Model, ML Training
- **Saad Saeed** – Node.js Integration

Final Year Project – BS Software Engineering  
Department of Information Technology
University of Haripur

---
