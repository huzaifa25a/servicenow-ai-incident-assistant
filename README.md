# ServiceNow AI Incident Assistant

A proof-of-concept automation built on the ServiceNow platform that generates troubleshooting suggestions when a new IT incident is created.

The system reads the incident description and automatically adds a suggested resolution to the work notes using server-side scripting.

This project demonstrates workflow automation and AI integration concepts within ServiceNow.

---

## Features

• Automatic incident analysis on creation  
• Business Rule automation on the Incident table  
• Server-side JavaScript scripting  
• Automated troubleshooting suggestions added to Work Notes  
• Designed as a foundation for AI-powered IT support assistants

---

## Architecture

User creates Incident  
↓  
ServiceNow Business Rule triggers on insert  
↓  
Incident description is processed  
↓  
AI suggestion generated  
↓  
Suggestion written to Work Notes

---

## Business Rule Script

```javascript
(function executeRule(current, previous) {

var desc = current.description.toString();

var suggestion = "AI Suggested Resolution based on issue: " + desc +
". Please restart the device and check network configuration.";

current.work_notes = suggestion;

})(current, previous);

```

---

Example OpenAI Integration (Concept)

In a production scenario, ServiceNow can call the OpenAI API to generate intelligent troubleshooting suggestions.

Example server-side integration:
```javascript
var request = new sn_ws.RESTMessageV2();
request.setEndpoint("https://api.openai.com/v1/chat/completions");
request.setHttpMethod("POST");

request.setRequestHeader("Authorization", "Bearer YOUR_OPENAI_API_KEY");
request.setRequestHeader("Content-Type", "application/json");

var body = {
  model: "gpt-4o-mini",
  messages: [
    {
      role: "user",
      content: "Suggest troubleshooting steps for this IT issue: " + current.description
    }
  ]
};

request.setRequestBody(JSON.stringify(body));

var response = request.execute();
var responseBody = response.getBody();
```

---

## Technologies Used

• ServiceNow Platform  
• Incident Management (ITSM)  
• Business Rules  
• Server-side JavaScript  
• REST API Integration


---

## Screenshots
1. Business Rule
<img width="1902" height="1079" alt="business-rule" src="https://github.com/user-attachments/assets/240e7be3-50db-4ad5-b417-d8ba610b89a6" />

2. Script
<img width="1898" height="566" alt="script" src="https://github.com/user-attachments/assets/97766dfa-7e68-46dc-a5e6-7fb1b7fe8813" />

3. Incident
<img width="1887" height="1078" alt="incident" src="https://github.com/user-attachments/assets/8a2b2b08-92c4-4db7-b922-69791402d8b5" />

4. Activity Stream
<img width="1887" height="510" alt="activity-stream" src="https://github.com/user-attachments/assets/f99cc7de-9d93-419e-99f7-9e460bb1f086" />

---

## Future Improvements

• Real OpenAI API integration  
• Dynamic AI troubleshooting suggestions  
• Incident classification using AI  
• Automated assignment recommendations  

---

## Author
Huzaifa Pachisa

Full Stack Developer | ServiceNow Enthusiast
