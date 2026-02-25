# EmailJS Setup Guide for NutriFitTrack Feedback Form

This guide will help you set up EmailJS to receive feedback emails from your website.

## Why EmailJS?

EmailJS is perfect for static websites because:
- ✅ Works with Vercel and all static hosting
- ✅ Free tier includes 200 emails/month
- ✅ No backend server required
- ✅ Easy to set up (5 minutes)
- ✅ Secure (API keys are public-safe)

## Step-by-Step Setup

### 1. Create an EmailJS Account

1. Go to [https://www.emailjs.com/](https://www.emailjs.com/)
2. Click "Sign Up" and create a free account
3. Verify your email address

### 2. Add an Email Service

1. Go to the [Email Services](https://dashboard.emailjs.com/admin/integration) page
2. Click "Add New Service"
3. Choose your email provider (Gmail, Outlook, etc.)
4. Follow the instructions to connect your email
5. **Copy your Service ID** (e.g., `service_abc123`)

### 3. Create an Email Template

1. Go to the [Email Templates](https://dashboard.emailjs.com/admin/templates) page
2. Click "Create New Template"
3. Use this template content:

**Template Name:** `feedback_template`

**Subject:** `NutriFitTrack Feedback: {{feedback_type}}`

**Content (HTML):**
```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: Arial, sans-serif;
      line-height: 1.6;
      color: #333;
    }
    .container {
      max-width: 600px;
      margin: 0 auto;
      padding: 20px;
    }
    .header {
      background: #3A5A40;
      color: white;
      padding: 20px;
      border-radius: 8px 8px 0 0;
    }
    .content {
      background: #f9f9f9;
      padding: 20px;
      border: 1px solid #e0e0e0;
      border-radius: 0 0 8px 8px;
    }
    .field {
      margin-bottom: 15px;
    }
    .label {
      font-weight: bold;
      color: #3A5A40;
    }
    .value {
      background: white;
      padding: 10px;
      border-radius: 4px;
      margin-top: 5px;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="header">
      <h2>New Feedback from NutriFitTrack</h2>
    </div>
    <div class="content">
      <div class="field">
        <div class="label">Feedback Type:</div>
        <div class="value">{{feedback_type}}</div>
      </div>
      
      <div class="field">
        <div class="label">Name:</div>
        <div class="value">{{from_name}}</div>
      </div>
      
      <div class="field">
        <div class="label">Email:</div>
        <div class="value">{{from_email}}</div>
      </div>
      
      <div class="field">
        <div class="label">Message:</div>
        <div class="value">{{message}}</div>
      </div>
      
      <div class="field">
        <div class="label">Submitted:</div>
        <div class="value">{{submission_date}}</div>
      </div>
    </div>
  </div>
</body>
</html>
```

4. Click "Save"
5. **Copy your Template ID** (e.g., `template_xyz789`)

### 4. Get Your Public Key

1. Go to [Account Settings](https://dashboard.emailjs.com/admin/account)
2. Find your **Public Key** (e.g., `AbCdEfGhIjKlMnOp`)
3. Copy it

### 5. Update Your Website Code

Open `feedback.html` and replace these three values:

```javascript
// Line 431: Replace YOUR_PUBLIC_KEY
emailjs.init('YOUR_PUBLIC_KEY'); // Replace with your actual public key

// Line 449-450: Replace YOUR_SERVICE_ID and YOUR_TEMPLATE_ID
const response = await emailjs.send(
  'YOUR_SERVICE_ID',    // Replace with your service ID
  'YOUR_TEMPLATE_ID',   // Replace with your template ID
  templateParams
);
```

**Example after replacement:**
```javascript
emailjs.init('AbCdEfGhIjKlMnOp');

const response = await emailjs.send(
  'service_abc123',
  'template_xyz789',
  templateParams
);
```

### 6. Test Your Form

1. Deploy your website to Vercel
2. Go to your feedback page
3. Fill out the form and submit
4. Check your email inbox for the feedback

## Troubleshooting

### Not receiving emails?

1. **Check spam folder** - First emails might go to spam
2. **Verify email service** - Make sure your email service is connected in EmailJS dashboard
3. **Check browser console** - Look for error messages
4. **Test template** - Use the "Test" button in EmailJS template editor
5. **Check quota** - Free tier has 200 emails/month limit

### Common Errors

**"Invalid public key"**
- Make sure you copied the public key correctly
- Check for extra spaces or quotes

**"Service not found"**
- Verify your Service ID is correct
- Make sure the service is active in your dashboard

**"Template not found"**
- Verify your Template ID is correct
- Make sure the template is saved

## Email Customization

You can customize the email template in the EmailJS dashboard:
- Change colors and styling
- Add your logo
- Modify the layout
- Add more fields

## Upgrade Options

If you need more than 200 emails/month:
- **Personal Plan**: $7/month - 1,000 emails
- **Professional Plan**: $15/month - 5,000 emails

## Security Notes

- ✅ EmailJS public key is safe to expose in frontend code
- ✅ Rate limiting is built-in to prevent abuse
- ✅ You can add domain whitelist in EmailJS settings
- ✅ No sensitive API keys are exposed

## Support

- EmailJS Documentation: https://www.emailjs.com/docs/
- EmailJS Support: https://www.emailjs.com/support/

---

That's it! Your feedback form is now ready to receive emails. 🎉
