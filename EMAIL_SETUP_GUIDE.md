# Email Setup Guide for Wedding Website

## Option 1: EmailJS (Recommended - Easiest)

EmailJS is the simplest solution that works directly with your current Google Forms setup.

### Step 1: Create EmailJS Account
1. Go to [EmailJS.com](https://www.emailjs.com/)
2. Sign up for a free account
3. Verify your email address

### Step 2: Connect Your Email Service
1. In EmailJS dashboard, go to **Email Services**
2. Click **Add New Service**
3. Choose **Gmail** (or your preferred email provider)
4. Follow the authentication steps
5. Note down your **Service ID** (e.g., `service_abc123`)

### Step 3: Create Email Template
1. Go to **Email Templates**
2. Click **Create New Template**
3. Use this template:

**Subject:** `RSVP Confirmation - Megan & Danté's Wedding`

**Content:**
```
Dear {{guest_name}},

Thank you for your RSVP to our wedding!

Wedding Details:
Date: {{wedding_date}}
Couple: {{couple_names}}

Your RSVP Details:
Number of Guests: {{guest_count}}

Guest Information:
{{guest_info}}

We're so excited to celebrate with you on February 21st, 2026!

With love,
Megan & Danté
```

4. Note down your **Template ID** (e.g., `template_xyz789`)

### Step 4: Get Your Public Key
1. Go to **Account** → **General**
2. Copy your **Public Key** (e.g., `user_abc123def456`)

### Step 5: Update Your Website
Replace these values in your `index.html`:

```javascript
// Line 1553: Replace with your actual public key
emailjs.init("YOUR_EMAILJS_PUBLIC_KEY");

// Line 1584: Replace with your actual service and template IDs
emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', templateParams)
```

### Step 6: Test
1. Submit a test RSVP
2. Check that you receive the confirmation email
3. Verify the email contains the correct guest information

---

## Option 2: Google Apps Script (Advanced - Gmail Integration)

This solution uses Google Apps Script to send emails directly from your Gmail account when someone submits the Google Form.

### Step 1: Create Google Apps Script
1. Go to [script.google.com](https://script.google.com)
2. Click **New Project**
3. Replace the default code with this:

```javascript
function onFormSubmit(e) {
  // Get the form response data
  const responses = e.values;
  const email = responses[1]; // Adjust index based on your form structure
  const guestCount = responses[2];
  
  // Prepare guest information
  let guestInfo = '';
  for (let i = 3; i < responses.length; i += 3) {
    const guestName = responses[i];
    const dietary = responses[i + 1];
    const attending = responses[i + 2];
    
    if (guestName) {
      guestInfo += `• ${guestName}`;
      if (attending) guestInfo += ` (${attending})`;
      if (dietary) guestInfo += ` - Dietary: ${dietary}`;
      guestInfo += '\n';
    }
  }
  
  // Create email content
  const subject = 'RSVP Confirmation - Megan & Danté\'s Wedding';
  const body = `
Dear ${email.split('@')[0]},

Thank you for your RSVP to our wedding!

Wedding Details:
Date: February 21st, 2026
Couple: Megan & Danté

Your RSVP Details:
Number of Guests: ${guestCount}

Guest Information:
${guestInfo}

We're so excited to celebrate with you on February 21st, 2026!

With love,
Megan & Danté
  `;
  
  // Send email
  GmailApp.sendEmail(email, subject, body);
  
  // Also send a copy to yourself
  GmailApp.sendEmail('your-email@gmail.com', `New RSVP from ${email}`, body);
}
```

### Step 2: Set Up Trigger
1. In your Apps Script project, click **Triggers** (clock icon)
2. Click **Add Trigger**
3. Set:
   - Function: `onFormSubmit`
   - Event source: `From form`
   - Event type: `On form submit`
4. Save and authorize the script

### Step 3: Test
1. Submit a test RSVP through your form
2. Check that you receive the confirmation email
3. Check that you receive a copy notification

---

## Option 3: Google Forms Built-in Notifications

### Simple Setup (No Code Required)
1. In your Google Form, go to **Responses** tab
2. Click the three dots (⋮) next to the Google Sheets icon
3. Select **Get email notifications for new responses**
4. Enter your email address
5. You'll receive notifications when someone submits an RSVP

**Note:** This only notifies you, it doesn't send confirmation emails to guests.

---

## Comparison of Options

| Feature | EmailJS | Google Apps Script | Form Notifications |
|---------|---------|-------------------|-------------------|
| **Setup Difficulty** | Easy | Medium | Very Easy |
| **Guest Confirmation** | ✅ Yes | ✅ Yes | ❌ No |
| **Customization** | ✅ High | ✅ High | ❌ None |
| **Cost** | Free (200 emails/month) | Free | Free |
| **Reliability** | ✅ High | ✅ High | ✅ High |

## Recommendation

**For your needs, I recommend EmailJS** because:
- It's the easiest to set up
- It sends beautiful confirmation emails to guests
- It works perfectly with your existing Google Forms setup
- It's free for up to 200 emails per month
- No server setup required

## Troubleshooting

### EmailJS Issues
- **Emails not sending**: Check your service ID and template ID
- **Template variables not working**: Ensure variable names match exactly
- **Authentication errors**: Re-authenticate your email service

### Google Apps Script Issues
- **Trigger not firing**: Check that the trigger is set to "On form submit"
- **Permission errors**: Re-authorize the script
- **Email not sending**: Check that Gmail API is enabled

### General Issues
- **Form not submitting**: Check browser console for errors
- **Missing data**: Verify your Google Form entry IDs are correct
- **CORS errors**: These are normal with Google Forms and won't affect functionality

## Next Steps

1. Choose your preferred option (EmailJS recommended)
2. Follow the setup steps
3. Test with a few RSVPs
4. Monitor the first few submissions to ensure everything works correctly

Need help with any of these steps? Let me know!
