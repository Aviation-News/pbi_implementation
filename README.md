# Power BI Embedded Flask Application

This application provides a streamlined way to embed Power BI reports in a web application using Flask as the backend server. It handles authentication with Azure AD, acquires the necessary embed tokens, and renders the Power BI report in a responsive web interface.


## 🚀 Features

- **Azure AD Integration**: Securely authenticates with Azure AD to access Power BI APIs
- **Embed Token Generation**: Automatically handles the acquisition of embed tokens
- **Responsive UI**: Clean, modern interface that works on desktop and mobile devices
- **Debug Information**: Helpful diagnostics for troubleshooting
- **API Endpoints**: Test and health check endpoints for monitoring and validation
- **CORS Support**: Built-in Cross-Origin Resource Sharing for frontend applications

## 📋 Requirements

- Python 3.6+
- Flask and Flask-CORS
- Power BI Pro or Premium account
- Azure AD application with appropriate permissions
- Power BI workspace with at least one report

## ⚙️ Configuration

The application uses the following configuration for connecting to Power BI:

```python
CONFIG = {
  'tenant_id': '65693725-b6ed-4482-838d-454f6f79eafb',
  'client_id': '8264d2da-a712-455b-bb14-6e10d4db8676',
  'client_secret': 'gH68Q~DVK4FHki2hwdgOC4we8tF3nZMsM50FhcC9',
  'group_id': '77200bef-3c01-4ece-b20a-10de91382e51',
  'report_id': 'df36791a-3629-4b43-b795-9ba2229f37be'
}
```

> **Security Note**: In a production environment, store sensitive information like `client_secret` in environment variables or a secure configuration management system.

## 🛠️ Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/powerbi-flask-embed.git
   cd powerbi-flask-embed
   ```

2. Install required packages:
   ```bash
   pip install flask flask-cors requests
   ```

3. Update the `CONFIG` dictionary in `app.py` with your Azure AD and Power BI details:
   - `tenant_id`: Your Azure AD tenant ID
   - `client_id`: Your Azure AD application (client) ID
   - `client_secret`: Your Azure AD application client secret
   - `group_id`: Your Power BI workspace/group ID
   - `report_id`: The ID of the Power BI report to embed

## 🏃‍♂️ Running the Application

Start the application with:

```bash
python app.py
```

The application will start and be available at:

- **Main App**: http://localhost:8080/
- **Test API**: http://localhost:8080/test
- **Health Check**: http://localhost:8080/health

## 🧩 Architecture

The application flow works as follows:

1. **Authentication**: The backend authenticates with Azure AD using OAuth 2.0 client credentials flow
2. **Token Acquisition**: The application requests an embed token from the Power BI REST API
3. **Report Details**: The application fetches report details like the embed URL
4. **Frontend Embedding**: The JavaScript frontend uses the Power BI JavaScript SDK to render the report

## 📚 API Endpoints

### Main Page (`/`)

Renders the embedded Power BI report in a responsive web interface with debug information.

### Test Endpoint (`/test`)

Returns a JSON response with token generation information, useful for testing your configuration:

```json
{
  "success": true,
  "message": "✅ Embed token generated successfully!",
  "data": {
    "token_length": 1245,
    "embed_url": "https://app.powerbi.com/reportEmbed...",
    "report_id": "df36791a-3629-4b43-b795-9ba2229f37be",
    "token_preview": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6I..."
  },
  "config": {
    "tenant_id": "65693725-b6ed-4482-838d-454f6f79eafb",
    "client_id": "8264d2da-a712-455b-bb14-6e10d4db8676",
    "group_id": "77200bef-3c01-4ece-b20a-10de91382e51",
    "report_id": "df36791a-3629-4b43-b795-9ba2229f37be"
  }
}
```

### Health Check (`/health`)

Returns application health status information:

```json
{
  "status": "healthy",
  "app": "Power BI Embedded Demo",
  "port": 8080,
  "endpoints": {
    "main": "http://localhost:8080/",
    "test": "http://localhost:8080/test",
    "health": "http://localhost:8080/health"
  }
}
```

## 🔧 Troubleshooting

If you encounter issues:

1. **Check backend logs**: Look for errors in the Flask console output
2. **Verify credentials**: Ensure your Azure AD credentials are correct
3. **Check permissions**: Make sure your Azure AD app has appropriate Power BI API permissions
4. **Test with `/test` endpoint**: Use the test endpoint to verify token generation
5. **Browser console**: Check for JavaScript errors in the browser console
6. **Network tab**: Inspect network requests in browser developer tools

## 🔒 Security Considerations

- **Credentials**: Never expose client secrets in frontend code
- **HTTPS**: Use HTTPS in production to protect tokens and credentials
- **Token Expiration**: Be aware that embed tokens expire (typically after 1 hour)
- **Scoped Access**: Use the minimum necessary permissions for your Azure AD application
- **Row-Level Security**: Consider implementing RLS for data protection if needed

## ⚡ Advanced Customization

The Power BI report embedding can be customized in several ways:

1. **Filtering**: Add pre-defined filters to show specific data
2. **UI Controls**: Customize which UI elements are visible (filter pane, page navigation)
3. **Themes**: Apply custom themes to match your application
4. **Event Handling**: Add custom handlers for report events (loaded, rendered, error)

See the [Power BI JavaScript SDK documentation](https://github.com/microsoft/PowerBI-JavaScript/wiki/Embedding-Basics) for more customization options.

## 📚 Resources

- [Power BI REST API Documentation](https://docs.microsoft.com/en-us/rest/api/power-bi/)
- [Power BI Embedded Analytics Documentation](https://docs.microsoft.com/en-us/power-bi/developer/embedded/)
- [Power BI JavaScript SDK](https://github.com/microsoft/PowerBI-JavaScript)
- [Azure AD Authentication for Apps](https://docs.microsoft.com/en-us/azure/active-directory/develop/)
- [Flask Documentation](https://flask.palletsprojects.com/)

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

Created with ❤️ for Power BI developers
