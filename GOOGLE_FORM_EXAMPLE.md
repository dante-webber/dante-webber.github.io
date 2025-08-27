# Google Form Structure Example

Here's exactly how your Google Form should be structured:

## Form Title
**Wedding RSVP - Megan & Danté**

## Questions (in order):

### 1. Email Address
- **Question Type**: Short answer
- **Required**: Yes
- **Question**: "Email Address"

### 2. Number of Guests
- **Question Type**: Short answer  
- **Required**: Yes
- **Question**: "Number of Guests"

### 3. Guest 1 Name
- **Question Type**: Short answer
- **Required**: Yes
- **Question**: "Guest 1 Name"

### 4. Guest 1 Dietary Requirements
- **Question Type**: Short answer
- **Required**: No
- **Question**: "Guest 1 Dietary Requirements/Allergies"

### 5. Guest 1 Attending
- **Question Type**: Multiple choice
- **Required**: Yes
- **Question**: "Will Guest 1 be attending?"
- **Options**: 
  - Yes
  - No

### 6. Guest 2 Name
- **Question Type**: Short answer
- **Required**: No
- **Question**: "Guest 2 Name"

### 7. Guest 2 Dietary Requirements
- **Question Type**: Short answer
- **Required**: No
- **Question**: "Guest 2 Dietary Requirements/Allergies"

### 8. Guest 2 Attending
- **Question Type**: Multiple choice
- **Required**: No
- **Question**: "Will Guest 2 be attending?"
- **Options**:
  - Yes
  - No

### Continue for Guests 3-10...
Repeat the same pattern for each additional guest.

## Form Settings

1. **General Settings**:
   - Collect email addresses: Yes
   - Limit to 1 response: No
   - Show progress bar: Yes

2. **Presentation**:
   - Show link to submit another response: No
   - Confirmation message: "Thank you for your RSVP! We look forward to celebrating with you!"

3. **Responses**:
   - Accepting responses: Yes
   - Response receipts: Yes

## Expected Entry IDs

After creating this form and linking it to a Google Sheet, your column headers will look something like this:

```
Timestamp | Email Address | Number of Guests | Guest 1 Name | Guest 1 Dietary Requirements/Allergies | Will Guest 1 be attending? | Guest 2 Name | Guest 2 Dietary Requirements/Allergies | Will Guest 2 be attending? | ...
entry.1234567890 | entry.0987654321 | entry.1111111111 | entry.2222222222 | entry.3333333333 | entry.4444444444 | entry.5555555555 | entry.6666666666 | entry.7777777777 | ...
```

**Note**: The actual entry IDs will be different numbers. You need to copy these from your Google Sheet column headers.
