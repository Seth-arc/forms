# EmailJS Dual Email Setup Guide

## ✅ Current Status
- **Service ID**: `service_fg5k8q8` (already configured)
- **Public Key**: `tHLlMDU6cDEkdxBfg` (already updated in both forms)
- **4 Email Templates**: Ready to upload to EmailJS

## 📧 Templates to Create in EmailJS Dashboard

### 1. Training Inquiry - Internal Notification
- **Template Name**: "Training Inquiry - Internal"
- **Template Content**: Copy from `AidData_Training_Inquiry_EmailJS_Template.html`
- **Recipients**: training@aiddata.org
- **Template ID**: `template_pzpfatt`

### 2. Training Inquiry - User Confirmation  
- **Template Name**: "Training Inquiry - User Confirmation"
- **Template Content**: Copy from `Training_Inquiry_User_Confirmation_Template.html`
- **Recipients**: User's email address
- **Template ID**: `template_au0d4yd`

### 3. Scholarship Request - Internal Notification
- **Template Name**: "Scholarship Request - Internal"
- **Template Content**: Copy from `Scholarship_Request_Internal_Template.html`
- **Recipients**: training@aiddata.org
- **Template ID**: `template_b8otaj6`

### 4. Scholarship Request - User Confirmation
- **Template Name**: "Scholarship Request - User Confirmation"
- **Template Content**: Copy from `Scholarship_Request_User_Confirmation_Template.html`
- **Recipients**: User's email address
- **Template ID**: `template_xvb981w`

## 🔧 Form Updates Required

### Professional Development Form Updates

**Replace this section in `professional_development_inquiry.html`:**

```javascript
// Current single email (around line 1540)
const response = await emailjs.send(
    'service_fg5k8q8',
    'YOUR_PROFESSIONAL_TEMPLATE_ID',
    {
        // existing data structure
    }
);
```

**With this dual email system:**

```javascript
try {
    // Send internal notification to training team
    await emailjs.send(
        'service_fg5k8q8',
        'template_pzpfatt',
        {
            to_email: 'training@aiddata.org',
            from_name: data.firstName + ' ' + data.lastName,
            from_email: data.email,
            subject: 'Professional Development Training Inquiry - ' + data.organizationName,
            
            // Organization Information
            organization_name: data.organizationName,
            organization_type: data.organizationType,
            organization_size: data.organizationSize || 'Not specified',
            country: data.country,
            website: data.website || 'Not provided',
            
            // Contact Information
            first_name: data.firstName,
            last_name: data.lastName,
            email: data.email,
            phone: data.phone || 'Not provided',
            job_title: data.jobTitle,
            
            // Training Requirements
            training_topic: data.trainingTopic,
            training_delivery: selectedTrainingType,
            participant_count: data.participantCount,
            timeline: data.timeline,
            
            // Additional Information
            additional_info: data.additionalInfo || 'None provided',
            hear_about: data.hearAbout || 'Not specified',
            
            // Timestamp
            submission_date: new Date().toLocaleString()
        }
    );

    // Send confirmation email to user
    await emailjs.send(
        'service_fg5k8q8',
        'template_au0d4yd',
        {
            to_email: data.email,
            from_name: 'AidData Training Team',
            from_email: 'training@aiddata.org',
            subject: 'Training Inquiry Confirmation - ' + data.organizationName,
            
            // User-relevant information only
            first_name: data.firstName,
            last_name: data.lastName,
            organization_name: data.organizationName,
            training_topic: data.trainingTopic,
            training_delivery: selectedTrainingType,
            participant_count: data.participantCount,
            submission_date: new Date().toLocaleString()
        }
    );

    // Show success message (existing code)
    loading.style.display = 'none';
    successMessage.style.display = 'block';
    // ... rest of success handling
    
} catch (error) {
    console.error('Error sending emails:', error);
    // ... existing error handling
}
```

### Scholarship Form Updates

**Replace this section in `scholarship_form.html`:**

```javascript
// Current single email (around line 1535)
const response = await emailjs.send(
    'YOUR_SERVICE_ID',
    'YOUR_SCHOLARSHIP_TEMPLATE_ID',
    {
        // existing data structure
    }
);
```

**With this dual email system:**

```javascript
try {
    // Send internal notification to training team
    await emailjs.send(
        'service_fg5k8q8',
        'template_b8otaj6',
        {
            to_email: 'training@aiddata.org',
            from_name: data.firstName + ' ' + data.lastName,
            from_email: data.email,
            subject: 'Scholarship Application - ' + data.firstName + ' ' + data.lastName,
            
            // All scholarship form data
            first_name: data.firstName,
            last_name: data.lastName,
            date_of_birth: data.dateOfBirth,
            email: data.email,
            phone: data.phone || 'Not provided',
            country: data.country,
            city: data.city,
            current_position: data.currentPosition,
            organization: data.organization,
            experience: data.experience || 'Not specified',
            sector: data.sector,
            education: data.education,
            field_of_study: data.fieldOfStudy || 'Not provided',
            motivation: data.motivation,
            experience_data: data.experience_data || 'None specified',
            expectations: data.expectations,
            additional_info: data.additional_info || 'None provided',
            hear_about: data.hear_about || 'Not specified',
            scholarship_priority: data.scholarshipPriority || 'Standard',
            submission_date: new Date().toLocaleString()
        }
    );

    // Send confirmation email to user
    await emailjs.send(
        'service_fg5k8q8',
        'template_xvb981w',
        {
            to_email: data.email,
            from_name: 'AidData Training Team',
            from_email: 'training@aiddata.org',
            subject: 'Scholarship Application Confirmation',
            
            // User-relevant information only
            first_name: data.firstName,
            last_name: data.lastName,
            country: data.country,
            current_position: data.currentPosition,
            organization: data.organization,
            submission_date: new Date().toLocaleString()
        }
    );

    // Show success message (existing code)
    loading.style.display = 'none';
    successMessage.style.display = 'block';
    // ... rest of success handling
    
} catch (error) {
    console.error('Error sending emails:', error);
    // ... existing error handling
}
```

## 📝 Implementation Steps

### Step 1: Create Templates in EmailJS
1. Go to your EmailJS dashboard
2. Create 4 new email templates
3. Copy HTML content from each template file
4. Note down the Template IDs

### Step 2: Update Form JavaScript
1. Replace the template IDs in the code above with your actual IDs
2. Update both forms with the dual email system
3. Test thoroughly

### Step 3: Test Email Flow
1. Submit test forms
2. Verify both emails are sent:
   - Internal team receives detailed notification
   - User receives confirmation email
3. Check email formatting and content

## 🎯 Expected Results

**When someone submits a Training Inquiry:**
- AidData team gets detailed inquiry with all form data
- User gets confirmation with next steps and consultation link

**When someone submits a Scholarship Application:**
- AidData team gets complete application details for review
- User gets confirmation with review timeline and course info

## ✅ Template IDs Configured

Your EmailJS template IDs are now configured:
- **TRAINING_INTERNAL_TEMPLATE_ID**: `template_pzpfatt`
- **TRAINING_USER_TEMPLATE_ID**: `template_au0d4yd`
- **SCHOLARSHIP_INTERNAL_TEMPLATE_ID**: `template_b8otaj6`
- **SCHOLARSHIP_USER_TEMPLATE_ID**: `template_xvb981w`

## ✅ Benefits of This Setup

1. **Professional user experience** - Immediate confirmation emails
2. **Organized internal workflow** - Detailed notifications for follow-up
3. **Reduced support queries** - Users know their submission was received
4. **Consistent branding** - All emails match AidData design standards
5. **Clear expectations** - Users know exactly what happens next
