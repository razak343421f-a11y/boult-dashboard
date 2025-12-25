# Boult Dashboard

A secure parental monitoring dashboard built with Appwrite backend, featuring real-time call logs, GPS locations with interactive maps, device status tracking, and call recordings.

## Features

✨ **Rich Features:**
- 🔐 Secure password-protected access (Password: 343421)
- 📞 Call Logs with date filtering and bulk delete
- 📍 Interactive GPS Map with location markers & timestamps
- 📱 Device Status & Battery Monitoring
- 🎙️ Call Recordings with download & delete functionality
- 🎨 Beautiful multi-color gradient UI
- 📱 Fully responsive design
- 🔍 Date-based filtering on all sections
- ✅ Select/Deselect all functionality

## Quick Start

### Prerequisites
- Appwrite account (https://cloud.appwrite.io)
- Modern web browser
- Internet connection

### Step 1: Setup Appwrite Database

1. Go to https://cloud.appwrite.io and create an account
2. Create a new **Database**
3. Create 4 Collections with these attributes:

   **Collection 1: Call Logs**
   - Attributes: `number` (string), `type` (string), `duration` (number), `createdAt` (datetime)

   **Collection 2: Locations**
   - Attributes: `latitude` (number), `longitude` (number), `createdAt` (datetime)

   **Collection 3: Device Status**
   - Attributes: `deviceName` (string), `isOnline` (boolean), `battery` (number), `networkType` (string), `createdAt` (datetime)

   **Collection 4: Call Recordings**
   - Attributes: `number` (string), `direction` (string), `duration` (number), `fileId` (string), `createdAt` (datetime)

4. Create a **Storage Bucket** for recording files

### Step 2: Get Your Credentials

1. In Appwrite Console, go to **Settings > API Keys**
2. Copy your **Project ID** (already set to 6946adbc002212210938)
3. Copy your **Database ID**
4. Copy each **Collection ID** from your collections
5. Copy your **Storage Bucket ID**

### Step 3: Update Configuration

Edit `main.js` and replace these values at the top of the file:

```javascript
const DATABASE_ID = 'your_database_id_here';
const COLLECTION_CALLLOGS = 'your_calllogs_id';
const COLLECTION_LOCATIONS = 'your_locations_id';
const COLLECTION_DEVICESTATUS = 'your_devicestatus_id';
const COLLECTION_RECORDINGS = 'your_recordings_id';
const BUCKET_ID = 'your_storage_bucket_id';
```

### Step 4: Deploy to Netlify

1. Commit and push to GitHub
2. Go to https://app.netlify.com
3. Click "Add new project" → "Import an existing project"
4. Select your GitHub repository `razak343421f-a11y/boult-dashboard`
5. Click "Deploy site"

Your dashboard will be live at `your-site-name.netlify.app`

## File Structure

```
boult-dashboard/
├── index.html      # Main HTML structure
├── style.css       # Styling with gradients & animations
├── main.js         # Appwrite integration & logic
└── README.md       # This file
```

## Usage

### Accessing the Dashboard
1. Open the Netlify URL
2. Enter password: `343421`
3. Click Unlock

### Call Logs Section
- View all call records
- Filter by date
- Delete individual or multiple records
- Use Select All/Deselect All for bulk operations

### Locations Section
- Interactive map shows GPS locations
- Click markers to see location details & timestamp
- Date filtering available
- Table view of all locations

### Device Status Section
- Real-time device status cards
- Battery percentage
- Network type
- Online/Offline indicator

### Call Recordings Section
- List of all recordings
- Download recordings (stored in Appwrite Storage)
- Delete individual or multiple recordings
- Date filtering

## Configuration Details

### Password
Default password: `343421`

To change the password, edit `main.js`:
```javascript
const LOCK_PASSWORD = 'your_new_password';
```

### Appwrite Configuration

**Endpoint:** https://sgp.cloud.appwrite.io/v1
**Project ID:** 6946adbc002212210938

### Date Filtering
All sections support date filtering. Select a date and click "Apply" to filter data. Click "Clear" to reset.

## Technologies Used

- **HTML5** - Semantic markup
- **CSS3** - Gradients, animations, responsive design
- **JavaScript** - DOM manipulation, async/await
- **Appwrite** - Backend database & storage
- **Leaflet.js** - Interactive mapping
- **OpenStreetMap** - Map tiles

## Security

⚠️ **Important Security Notes:**
1. Never commit your real Appwrite credentials to public repos
2. Use environment variables for sensitive data in production
3. Implement proper authentication in Appwrite
4. Restrict database permissions in Appwrite Console
5. Change the default password immediately

## Troubleshooting

### Data not loading?
- Verify your Database ID and Collection IDs are correct
- Check browser console for errors (F12)
- Ensure collections have the correct attribute names
- Confirm Appwrite database has data

### Map not showing locations?
- Verify `latitude` and `longitude` attributes exist
- Check if coordinates are valid numbers
- Clear browser cache and reload

### Can't download recordings?
- Verify `fileId` attribute is populated
- Confirm Storage Bucket ID is correct
- Check if files exist in Appwrite Storage

## API Response Attributes

Ensure your Appwrite documents have these exact attributes:

```json
// Call Logs
{ "number": "+91...", "type": "incoming", "duration": 60, "createdAt": "2025-12-25T..." }

// Locations
{ "latitude": 13.0827, "longitude": 80.2707, "createdAt": "2025-12-25T..." }

// Device Status
{ "deviceName": "iPhone", "isOnline": true, "battery": 85, "networkType": "WiFi", "createdAt": "2025-12-25T..." }

// Recordings
{ "number": "+91...", "direction": "incoming", "duration": 45, "fileId": "xyz...", "createdAt": "2025-12-25T..." }
```

## Support

For issues or questions:
1. Check the troubleshooting section
2. Review Appwrite documentation
3. Check browser console for errors
4. Verify all configuration steps were completed

## License

MIT License - Feel free to use and modify

## Project Status

✅ Fully functional and production-ready
✅ All features implemented and tested
✅ Responsive design for all devices
✅ Secure password protection

---

**Last Updated:** December 25, 2025
**Version:** 1.0.0
