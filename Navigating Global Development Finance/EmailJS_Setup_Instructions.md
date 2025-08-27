# EmailJS Setup Instructions for Scholarship Form

To enable the scholarship form to send emails automatically to training@aiddata.org and handle W&M email verification, you need to configure EmailJS. Follow these steps:

## 1. Create EmailJS Account

1. Go to [EmailJS.com](https://www.emailjs.com/)
2. Sign up for a free account
3. Verify your email address

## 2. Create Email Service

1. In your EmailJS dashboard, click "Add New Service"
2. Choose your email provider (Gmail, Outlook, etc.)
3. Follow the setup instructions for your chosen provider
4. Note down your **Service ID** (you'll need this later)

## 3. Create Email Templates

You need to create THREE templates:

### Template 1: Scholarship Application Template

1. Go to "Email Templates" in your dashboard
2. Click "Create New Template"
3. Name it "Scholarship Application Template"
4. Use this template content:

```html
Subject: {{scholarship_type}} Scholarship Application - {{from_name}}

Dear AidData Training Team,

A new {{scholarship_type}} scholarship application has been submitted for the Navigating Global Development Finance course.

SCHOLARSHIP VERIFICATION:
========================
Scholarship Type: {{scholarship_type}}
Verified W&M Email: {{verified_email}}
Verified Location: {{verified_location}}

APPLICANT DETAILS:
==================
Name: {{first_name}} {{last_name}}
Email: {{email}}
Phone: {{phone}}
Country: {{country}}
City: {{city}}

PROFESSIONAL BACKGROUND:
========================
Organization: {{organization}}
Position: {{position}}
Experience: {{experience}}
Sector: {{sector}}

EDUCATIONAL BACKGROUND:
=======================
Education Level: {{education}}
Field of Study: {{field_of_study}}

COURSE INTEREST & MOTIVATION:
=============================
Motivation:
{{motivation}}

Prior Experience:
{{experience_data}}

Expectations:
{{expectations}}

ADDITIONAL INFORMATION:
=======================
{{additional_info}}

How they heard about us: {{hear_about}}

Application submitted on: {{submission_date}}

---
This application was submitted through the AidData scholarship form.
Please review and respond to the applicant at: {{from_email}}
```

5. Save the template and note down your **Template ID**

### Template 2: W&M Email Verification Template

1. Click "Create New Template" again
2. Name it "W&M Email Verification Template"
3. Use this template content:

```html
Subject: W&M Scholarship Application - Verification Code

Dear William & Mary Community Member,

Thank you for your interest in the AidData Scholarship for the Navigating Global Development Finance course.

To complete your W&M Affiliation Scholarship application, please use the following verification code:

VERIFICATION CODE: {{verification_code}}

Please enter this 6-digit code in the scholarship application form to verify your W&M email address.

This code will expire in 15 minutes for security purposes.

If you did not request this verification code, please ignore this email.

Best regards,
AidData Training Team
training@aiddata.org

---
This is an automated verification email from the AidData scholarship application system.
```

4. Save the template and note down your **Verification Template ID**

### Template 3: Professional Development Inquiry Template

1. Click "Create New Template" again
2. Name it "Professional Development Inquiry Template"
3. Use this template content:

```html
Subject: Professional Development Training Inquiry - {{organization_name}}

Dear AidData Training Team,

A new professional development training inquiry has been submitted from {{organization_name}}.

ORGANIZATION INFORMATION:
========================
Organization: {{organization_name}}
Type: {{organization_type}}
Size: {{organization_size}}
Country: {{country}}
Website: {{website}}

CONTACT INFORMATION:
===================
Name: {{first_name}} {{last_name}}
Title: {{job_title}}
Email: {{email}}
Phone: {{phone}}

TRAINING REQUIREMENTS:
=====================
Training Topic: {{training_topic}}
Delivery Method: {{training_delivery}}
Participant Count: {{participant_count}}
Timeline: {{timeline}}

TRAINING OBJECTIVES:
===================
Objectives:
{{objectives}}

Current Knowledge Level: {{current_level}}

Customization Requirements:
{{customization}}

Additional Services: {{additional_services}}

ADDITIONAL INFORMATION:
======================
{{additional_info}}

How they heard about us: {{hear_about}}

Inquiry submitted on: {{submission_date}}

---
This inquiry was submitted through the AidData professional development form.
Please respond to the contact at: {{from_email}}
```

5. Save the template and note down your **Professional Development Template ID**

## 4. Get Your Public Key

1. Go to "Account" in your EmailJS dashboard
2. Find your **Public Key** in the API Keys section

## 5. Update the HTML Files

### For scholarship_form.html:

```javascript
// Replace line 931
emailjs.init("YOUR_PUBLIC_KEY"); // Replace with your actual public key

// Replace lines 1016-1017 (W&M verification email)
'YOUR_SERVICE_ID', // Replace with your actual service ID
'YOUR_VERIFICATION_TEMPLATE_ID', // Replace with your verification template ID

// Replace lines 1327-1328 (Application submission email)
'YOUR_SERVICE_ID', // Replace with your actual service ID
'YOUR_TEMPLATE_ID', // Replace with your main application template ID
```

### For professional_development_inquiry.html:

```javascript
// Replace line 607
emailjs.init("YOUR_PUBLIC_KEY"); // Replace with your actual public key

// Replace lines 802-803 (Professional development inquiry email)
'YOUR_SERVICE_ID', // Replace with your actual service ID
'YOUR_PROFESSIONAL_TEMPLATE_ID', // Replace with your professional development template ID
```

## 6. Test the Form

### Testing W&M Affiliation Scholarship:
1. Open `scholarship_form.html` in a web browser
2. Select "W&M Affiliation Scholarship"
3. Enter a test @wm.edu email address
4. Click "Send Code" and verify the verification email is received
5. Enter the verification code and continue to the application
6. Fill out the form and submit
7. Check if the application email arrives at training@aiddata.org

### Testing Global South Scholarship:
1. Open `scholarship_form.html` in a web browser
2. Select "Global South Scholarship"
3. Ensure you're in a Global South country location (or test location detection)
4. Verify location detection works correctly
5. Continue to the application form
6. Fill out the form and submit
7. Check if the application email arrives at training@aiddata.org

### Testing Professional Development Inquiry:
1. Open `professional_development_inquiry.html` in a web browser
2. Select a training delivery method (online, multimodal, or in-person)
3. Fill out all required organization and contact information
4. Complete training requirements and objectives
5. Submit the form
6. Check if the inquiry email arrives at training@aiddata.org

## Security Notes

- The public key is safe to expose in client-side code
- Consider setting up domain restrictions in EmailJS for added security
- Monitor your EmailJS usage to stay within free tier limits (200 emails/month)

## Troubleshooting

**Form not sending emails:**
- Check browser console for JavaScript errors
- Verify all three IDs (Service ID, Template ID, Public Key) are correct
- Ensure EmailJS service is properly connected to your email provider

**Emails going to spam:**
- Add your domain to EmailJS allowed domains
- Use a professional email service (Gmail, Outlook, etc.)
- Test with different email providers

**Template variables not working:**
- Ensure variable names in template match the data object keys
- Check for typos in variable names (case-sensitive)

## Support

- EmailJS Documentation: https://www.emailjs.com/docs/
- For form-specific issues, contact the developer
- For scholarship program questions, email training@aiddata.org
