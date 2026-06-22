# Arro Simple Form

[![NuGet](https://img.shields.io/nuget/v/ArroSimpleForm.svg)](https://www.nuget.org/packages/ArroSimpleForm/)
[![License](https://img.shields.io/badge/license-Commercial-blue.svg)](https://www.arroact.com)

**Arro Simple Form** is a powerful form builder for Umbraco CMS that enables users to create dynamic, customizable forms without writing any code. Seamlessly integrate forms into your Umbraco websites with automated data collection and email notifications.

## 🚀 Features

- **No-Code Form Builder** - Create and manage forms through an intuitive interface
- **Dynamic Form Fields** - Support for various field types (text, email, file uploads, etc.)
- **Data Collection** - Automatically save all form submissions to the database
- **Email Notifications** - Send automated emails on form submission with file attachments
- **File Upload Support** - Handle file uploads with Base64 encoding and storage
- **Redirect Actions** - Configure post-submission redirects
- **Tracking & Analytics** - Capture submission metadata (IP address, browser, page URL)
- **SMTP Integration** - Full integration with Umbraco's SMTP configuration
- **Umbraco 17 Compatible** - Built for .NET 10.0 and Umbraco CMS 17

## 📋 Requirements

- **Umbraco CMS**: Version 13.0.0 or higher
- **.NET**: Version 8.0 or higher
- **Database**: SQL Server

## 📦 Installation

Install the package via NuGet Package Manager:

```bash
dotnet add package ArroSimpleForm
```

Or via the NuGet Package Manager Console:

```powershell
Install-Package ArroSimpleForm
```

Or add it directly to your `.csproj` file:

```xml
<PackageReference Include="ArroSimpleForm" Version="13.0.0" />
```

## 🆕 Version 17.0.4 Updates

In version **17.0.4**, Arro Simple Form introduces new APIs designed for use with headless applications:

- **Form Fetch API**: Retrieve form data dynamically, including all defined fields.
- **Form Submission API**: Submit form data programmatically, enabling seamless integration in headless environments.

These APIs enhance the flexibility of Arro Simple Form, making it easier to integrate with modern headless CMS architectures.

## 📝 API Key Configuration

To access the APIs, configure the `FormsApiKey` in your `appsettings.json` file:

```json
"Arroact": {
    "FormsApiKey": "<yourkey>"
}
```

### Usage
Pass the API key as a header when consuming:

```header
X-Api-Key: <yourkey>
```

## 🆕 Version 17.0.4 Updates

### Example: Retrieve Form Data by ID or Name

#### By ID
```bash
GET /api/simpleform/form/{id}

Headers:
X-Api-Key: your-api-key

Response:
{
    "id": 123,
    "name": "Contact Us Form",
    "fields": [
        { "name": "email", "type": "text", "required": true },
        { "name": "message", "type": "textarea", "required": true }
    ]
}
```
#### By Name
```bash
GET /api/simpleform/form/name/{name}

Headers:
X-Api-Key: your-api-key

Response:
{
    "webFormFields": [
        {
            "id": 4,
            "type": "header",
            "subtype": "h1",
            "name": null,
            "label": "Header\n",
            "description": null,
            "placeholder": null,
            "value": null,
            "className": null,
            "style": null,
            "required": null,
            "min": null,
            "max": null,
            "maxlength": null,
            "rows": null,
            "multiple": null,
            "toggle": null,
            "inline": null,
            "other": null,
            "action": null,
            "actionRedirect": null,
            "actionSendEmail": null,
            "actionJavascript": null,
            "values": []
        },
        {
            "id": 5,
            "type": "text",
            "subtype": "text",
            "name": "text-1781617850498-0",
            "label": "Text Field\n",
            "description": null,
            "placeholder": null,
            "value": null,
            "className": "form-control",
            "style": null,
            "required": null,
            "min": null,
            "max": null,
            "maxlength": null,
            "rows": null,
            "multiple": null,
            "toggle": null,
            "inline": null,
            "other": null,
            "action": null,
            "actionRedirect": null,
            "actionSendEmail": null,
            "actionJavascript": null,
            "values": []
        }
    ]
}
```

```bash
GET /api/simpleform/form/{id}

Headers:
X-Api-Key: your-api-key

Response:
{
    "id": 123,
    "name": "Contact Us Form",
    "fields": [
        { "name": "email", "type": "text", "required": true },
        { "name": "message", "type": "textarea", "required": true }
    ]
}
```

#### Submit Form with Files
```javascript
// Request
const formData = new FormData();
formData.append('formId', 1);
formData.append('email', 'user@example.com');
formData.append('name', 'John Doe');
formData.append('files', fileInput.files[0]);

fetch('/api/simpleform/submit', {
  method: 'POST',
  body: formData
})

// Response (Success)
{
  "success": true,
  "submissionId": 12345,
  "message": "Form submitted successfully",
  "redirectUrl": "https://example.com/thank-you"
}
```


## ⚙️ Configuration

### SMTP Settings

Configure SMTP settings in your `appsettings.json` to enable email notifications:

```json
{
  "Umbraco": {
    "Cms": {
      "Global": {
        "Smtp": {
          "Host": "smtp.example.com",
          "Port": 587,
          "From": "noreply@example.com",
          "FromName": "Your Website",
          "Username": "your-smtp-username",
          "Password": "your-smtp-password",
          "SecureSocketOptions": "StartTLS"
        }
      }
    }
  }
}
```

**SecureSocketOptions** values:
- `Auto` - Auto-detect based on port
- `StartTLS` - Use STARTTLS
- `SSL` or `TLS` - Use SSL/TLS from connection
- `None` - No encryption

## 🎯 Usage

### 1. Create a Form

1. Navigate to the Arro Simple Form section in your Umbraco backoffice
2. Create a new form and configure your fields
3. Set up form actions (email notifications, redirects, etc.)
4. Save your form

### 2. Add Form to Your Page

Include the form in your Umbraco template or view:

```cshtml
@await Html.PartialAsync("FormView","yourFormName")
```

### 3. Configure Form Actions

Forms support multiple actions on submission:

- **Send Email** - Automatically send form data to specified recipients
- **Redirect** - Redirect users to a thank-you page or custom URL
- **Save Data** - All submissions are automatically saved to the database

### 4. View Submissions

Access form submissions through the Umbraco backoffice to:
- View all form entries
- Export data
- Track submission metadata (IP, browser, timestamp, page URL)


## 🔒 Security Features

- **Anti-Forgery Token** - Built-in CSRF protection
- **File Upload Validation** - Secure file handling with MIME type detection
- **IP Tracking** - Record submitter IP addresses
- **Data Encryption** - Files stored as Base64 encoded strings

## 🛠️ Advanced Features

### File Uploads

The form supports file uploads with:
- Multiple file attachments
- Automatic MIME type detection
- Base64 encoding for database storage
- Email attachment support

### Email Customization

Emails include:
- HTML formatted submission data
- All form fields in a structured table
- File attachments (if uploaded)
- Customizable subject lines
- Multiple recipients support

### Submission Tracking

Each submission captures:
- Form page URL
- Website URL
- Client IP address
- Browser information
- Submission timestamp
- Form processing logs


## 🤝 Support

For support, feature requests, or bug reports:

- **Website**: [https://www.arroact.com](https://www.arroact.com)
- **Company**: Arroact Technologies Pvt. Ltd.

## 📄 License

Copyright © Arroact Technologies Pvt. Ltd.

This is a commercial product. Please contact Arroact Technologies for licensing information.

## 🏢 About Arroact

Arroact Technologies Pvt. Ltd. specializes in developing powerful tools and extensions for Umbraco CMS, helping businesses build better web experiences.

---

**Made with ❤️ by [Arroact Technologies](https://www.arroact.com)**
