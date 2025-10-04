# Google Forms RSVP Setup Guide

## Overview
This guide will help you set up Google Forms to collect RSVP data from your wedding website. The form will automatically submit responses to a Google Form, which you can then view in a Google Sheet.

## Step 1: Create Your Google Form

1. Go to [Google Forms](https://forms.google.com)
2. Click "Blank" to create a new form
3. Title it "Wedding RSVP - Megan & Danté"

### Add Form Questions

Create the following questions in your form:

#### Basic Information
- **Email Address** (Short answer, required)
- **Number of Guests** (Short answer, required)

#### Guest Information (Repeat for each potential guest)
For Guest 1:
- **Guest 1 Name** (Short answer, required)
- **Guest 1 Dietary Requirements** (Short answer, optional)
- **Guest 1 Attending** (Multiple choice: Yes/No, required)

For Guest 2:
- **Guest 2 Name** (Short answer)
- **Guest 2 Dietary Requirements** (Short answer)
- **Guest 2 Attending** (Multiple choice: Yes/No)

Continue this pattern for up to 10 guests (Guest 3 through Guest 10).

## Step 2: Get Your Form ID

1. Click the **Send** button in your Google Form
2. Choose the **Link** tab
3. Copy the form URL
4. Extract the FORM_ID from the URL:
   ```
   https://docs.google.com/forms/d/FORM_ID/viewform
   ```

## Step 3: Get Field Entry IDs

### Method 1: Using Google Sheets (Recommended)
1. In your Google Form, click the **Responses** tab
2. Click the green **Google Sheets** icon
3. Choose "Create a new spreadsheet"
4. Submit a test response to your form
5. Go to the Google Sheet and look at the column headers
6. The entry IDs are in the column headers (e.g., "entry.1234567890")

### Method 2: Using Browser Developer Tools
1. Open your form in a browser
2. Right-click and select "View Page Source"
3. Search for `entry.` to find the entry IDs

## Step 4: Update Your Website Code

Replace the placeholder values in your `index.html` file:

### Replace the Form ID
Find this line:
```javascript
fetch('https://docs.google.com/forms/d/YOUR_GOOGLE_FORM_ID/formResponse', {
```

Replace `YOUR_GOOGLE_FORM_ID` with your actual form ID.

### Replace the Entry IDs
Find these lines and replace with your actual entry IDs:
```javascript
googleFormsData.append('entry.1234567890', email); // Email field ID
googleFormsData.append('entry.0987654321', guestCount); // Guest count field ID
```

For guest fields, replace the placeholder entry IDs:
```javascript
if (guestName) googleFormsData.append(`entry.${1111111111 + i}`, guestName);
if (dietary) googleFormsData.append(`entry.${2222222222 + i}`, dietary);
if (attending) googleFormsData.append(`entry.${3333333333 + i}`, attending);
```

## Step 5: Test Your Setup

1. Deploy your updated website
2. Submit a test RSVP
3. Check your Google Form responses to ensure data is being recorded
4. Verify the confirmation email is sent (if using EmailJS)

## Step 6: View Responses

You can view responses in two ways:
1. **Google Forms**: Click the "Responses" tab in your form
2. **Google Sheets**: Click the green Sheets icon to create a spreadsheet with all responses

## Troubleshooting

### Common Issues:

1. **Form not submitting**: Check that your form ID is correct
2. **Missing data**: Verify that entry IDs match your form fields
3. **CORS errors**: This is normal with Google Forms - the form will still submit
4. **No confirmation email**: Check your EmailJS configuration

### Testing Tips:

1. Submit test responses with different guest counts
2. Test with various dietary requirements
3. Test both "Yes" and "No" attendance responses
4. Check that the confirmation message appears after submission

## Security Notes

- Google Forms responses are public by default
- Consider setting your form to "Restrict to users in [your domain]" if using Google Workspace
- The form data will be visible to anyone with the form link

## Alternative: Using Google Apps Script

For more advanced functionality, you can use Google Apps Script to:
- Send custom confirmation emails
- Validate responses
- Integrate with other Google services
- Add custom logic for response processing

## Support

If you encounter issues:
1. Check the browser console for JavaScript errors
2. Verify all entry IDs are correct
3. Test with a simple form submission first
4. Ensure your Google Form is published and accessible
