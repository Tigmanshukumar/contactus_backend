# Contact Us Backend

A serverless contact form backend solution deployed on Netlify, providing a simple and efficient way to handle contact form submissions from your frontend applications.
- Student ID - 1401/INFI25/018

## 🌐 Live Demo

**[View Live Application](https://contactusbackend.netlify.app/)**

## 💻 Local Host
- Before Run in Local Host (http://localhost:3000/)

  **Replace The Code**
 ```bash
    <form method="GET" action="success.html" class="space-y-5">
   ```
 **TO**

 ```bash
   <form method="POST" action="/submit" class="space-y-5">
   ```
## 📋 Overview

This project provides a serverless backend solution for handling contact form submissions. Built with modern web technologies and deployed on Netlify, it offers a reliable, scalable, and cost-effective way to process contact forms without maintaining a traditional server infrastructure.

## ✨ Features

- **Serverless Architecture**: Powered by Netlify Functions for automatic scaling
- **Form Handling**: Process contact form submissions efficiently  
- **Email Integration**: Send email notifications when forms are submitted
- **API Endpoints**: RESTful API for form submission handling
- **Secure**: Built-in security features and validation
- **Zero Configuration Deployment**: Easy deployment with Netlify
- **Cost Effective**: Pay-per-use serverless pricing model

## 🚀 Getting Started

### Prerequisites

- Node.js (v14 or higher)
- npm or yarn package manager
- Netlify account (for deployment)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/contact-us-backend.git
   cd contact-us-backend
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Set up environment variables**
   Create a `.env` file in the root directory:
   ```env
   EMAIL_SERVICE_API_KEY=your_email_service_api_key
   SENDER_EMAIL=your-email@example.com
   RECIPIENT_EMAIL=contact@yourcompany.com
   ```

4. **Run locally**
   ```bash
   npm run dev
   # or
   netlify dev
   ```

## 📁 Project Structure

```
contact-us-backend/
├── netlify/
│   └── functions/
│       ├── contact.js          # Main contact form handler
│       └── send-email.js       # Email sending function
├── public/
│   ├── index.html             # Basic contact form UI
│   └── style.css              # Styling
├── package.json
├── netlify.toml              # Netlify configuration
├── .env.example              # Environment variables template
└── README.md
```

## 🛠️ API Endpoints

### POST `/api/contact`

Submit a contact form message.

**Request Body:**
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "subject": "General Inquiry",
  "message": "Hello, I have a question about your services."
}
```

**Response:**
```json
{
  "success": true,
  "message": "Message sent successfully!",
  "timestamp": "2025-08-11T10:30:00Z"
}
```

**Error Response:**
```json
{
  "success": false,
  "error": "Validation failed",
  "details": "Email is required"
}
```

## 🎨 Frontend Integration

### HTML Form Example

```html
<form id="contact-form">
  <input type="text" name="name" placeholder="Your Name" required>
  <input type="email" name="email" placeholder="Your Email" required>
  <input type="text" name="subject" placeholder="Subject" required>
  <textarea name="message" placeholder="Your Message" required></textarea>
  <button type="submit">Send Message</button>
</form>
```

### JavaScript Integration

```javascript
document.getElementById('contact-form').addEventListener('submit', async (e) => {
  e.preventDefault();
  
  const formData = new FormData(e.target);
  const data = Object.fromEntries(formData);
  
  try {
    const response = await fetch('https://contactusbackend.netlify.app/api/contact', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(data)
    });
    
    const result = await response.json();
    
    if (result.success) {
      alert('Message sent successfully!');
      e.target.reset();
    } else {
      alert('Error: ' + result.error);
    }
  } catch (error) {
    alert('Network error. Please try again.');
  }
});
```

### React Integration

```jsx
import { useState } from 'react';

const ContactForm = () => {
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    subject: '',
    message: ''
  });
  const [loading, setLoading] = useState(false);

  const handleSubmit = async (e) => {
    e.preventDefault();
    setLoading(true);
    
    try {
      const response = await fetch('https://contactusbackend.netlify.app/api/contact', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(formData)
      });
      
      const result = await response.json();
      
      if (result.success) {
        alert('Message sent!');
        setFormData({ name: '', email: '', subject: '', message: '' });
      }
    } catch (error) {
      console.error('Error:', error);
    } finally {
      setLoading(false);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      {/* Form fields */}
    </form>
  );
};
```

## 🚀 Deployment

### Deploy to Netlify

1. **Via Netlify CLI**
   ```bash
   npm install -g netlify-cli
   netlify login
   netlify deploy --prod
   ```

2. **Via GitHub Integration**
   - Connect your GitHub repository to Netlify
   - Set build command: `npm run build`
   - Set publish directory: `public`
   - Add environment variables in Netlify dashboard

3. **Via Drag & Drop**
   - Build your project: `npm run build`
   - Drag the `public` folder to Netlify dashboard

## ⚙️ Configuration

### Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `EMAIL_SERVICE_API_KEY` | API key for email service (SendGrid, Mailgun, etc.) | Yes |
| `SENDER_EMAIL` | Email address for sending notifications | Yes |
| `RECIPIENT_EMAIL` | Email address to receive contact form submissions | Yes |
| `ALLOWED_ORIGINS` | Comma-separated list of allowed origins for CORS | No |

### Netlify Configuration

The `netlify.toml` file contains deployment settings:

```toml
[build]
  functions = "netlify/functions"
  publish = "public"

[functions]
  node_bundler = "esbuild"

[[headers]]
  for = "/api/*"
  [headers.values]
    Access-Control-Allow-Origin = "*"
    Access-Control-Allow-Headers = "Content-Type"
    Access-Control-Allow-Methods = "GET, POST, OPTIONS"
```

## 🔒 Security Features

- **Input Validation**: Validates all form fields
- **Rate Limiting**: Prevents spam submissions
- **CORS Protection**: Configurable allowed origins
- **Email Sanitization**: Prevents email injection attacks
- **Environment Variables**: Sensitive data stored securely

## 🛡️ Error Handling

The backend includes comprehensive error handling:

- **Validation Errors**: Missing or invalid form fields
- **Rate Limit Errors**: Too many requests from same IP
- **Email Service Errors**: Issues with email delivery
- **Network Errors**: Connection timeouts and failures

## 🔧 Customization

### Adding New Fields

1. Update the validation schema in `netlify/functions/contact.js`
2. Modify the email template to include new fields
3. Update your frontend form accordingly

### Custom Email Templates

Modify the email template in the contact function:

```javascript
const emailTemplate = `
  <h2>New Contact Form Submission</h2>
  <p><strong>Name:</strong> ${name}</p>
  <p><strong>Email:</strong> ${email}</p>
  <p><strong>Subject:</strong> ${subject}</p>
  <p><strong>Message:</strong></p>
  <p>${message.replace(/\n/g, '<br>')}</p>
`;
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/new-feature`
3. Commit changes: `git commit -am 'Add new feature'`
4. Push to branch: `git push origin feature/new-feature`
5. Submit a pull request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📧 Support

If you have any questions or need help:

- Open an issue on GitHub
- Contact: [tigmanshukumar5@gmail.com]


## 🙏 Acknowledgments

- [Netlify](https://netlify.com) for serverless hosting
- [Netlify Functions](https://docs.netlify.com/functions/overview/) for backend functionality
- Community contributors and feedback

---

**Built with ❤️ using Netlify Functions**
