# Appwrite Setup Guide for Boult Dashboard

## Current Status

Your Boult Dashboard is **successfully deployed** on Netlify with all features ready:
- ✅ Interactive Locations Map (Leaflet.js)
- ✅ Call Logs with delete & bulk operations
- ✅ Call Recordings with download & delete
- ✅ Device Status tracking
- ✅ Password Lock (343421)

**However**: Data isn't showing because the **Appwrite collection IDs are not configured**.

## Why Data Isn't Showing

The JavaScript code in `main.js` tries to fetch data from Appwrite, but uses placeholder values:
```javascript
const DATABASE_ID = 'your_database_id_here';  // ← NOT CONFIGURED
const COLLECTION_CALLLOGS = 'your_calllogs_id';  // ← NOT CONFIGURED
```

When these are not real IDs, the app shows "Loading..." but can't fetch any data.

## Step-by-Step Setup

### Step 1: Create Appwrite Database & Collections

1. Go to **https://cloud.appwrite.io**
2. Sign in to your project
3. Go to **Databases** → Create a new database
4. Name it: `boult_db`
5. Copy the **Database ID** (save this!)

### Step 2: Create Required Collections

Inside your new database, create 4 collections:

#### Collection 1: call_logs
Attributes:
- `number` (String)
- `type` (String) - "incoming" or "outgoing"
- `duration` (Number) - seconds
- `createdAt` (DateTime) - auto-set to current time

#### Collection 2: locations
Attributes:
- `latitude` (Double/Decimal) or `lat`
- `longitude` (Double/Decimal) or `lng`
- `createdAt` (DateTime) - auto-set to current time

#### Collection 3: device_status
Attributes:
- `deviceName` (String)
- `isOnline` (Boolean)
- `battery` (Number) - 0-100
- `networkType` (String) - "WiFi", "4G", "LTE", etc.
- `createdAt` (DateTime)

#### Collection 4: call_recordings
Attributes:
- `number` (String)
- `direction` (String) - "incoming" or "outgoing"
- `duration` (Number)
- `fileId` (String) - Appwrite Storage file ID
- `createdAt` (DateTime)

### Step 3: Update main.js Configuration

Edit the `main.js` file in your repository (Line 5-14):

```javascript
const APPWRITE_ENDPOINT = 'https://sgp.cloud.appwrite.io/v1';
const APPWRITE_PROJECT = '6946adbc002212210938';

// Replace these with YOUR actual IDs from Appwrite
const DATABASE_ID = 'YOUR_DATABASE_ID_HERE';
const COLLECTION_CALLLOGS = 'YOUR_CALLLOGS_ID';
const COLLECTION_LOCATIONS = 'YOUR_LOCATIONS_ID';
const COLLECTION_DEVICESTATUS = 'YOUR_DEVICESTATUS_ID';
const COLLECTION_RECORDINGS = 'YOUR_RECORDINGS_ID';
const BUCKET_ID = 'YOUR_STORAGE_BUCKET_ID';
```

**How to find these IDs**:
1. In Appwrite Console, open your Database
2. Copy the **Database ID** from settings
3. For each Collection, click it and copy the **Collection ID**
4. For Storage, go to Storage → Copy the **Bucket ID**

### Step 4: Add Test Data (Optional)

Add sample data to test the dashboard:

1. Go to **Databases** → Select your database
2. Click **call_logs** collection
3. Click **+ Add Document**
4. Add a sample call:
```json
{
  "number": "+91-9876543210",
  "type": "incoming",
  "duration": 125,
  "createdAt": "2025-12-25T15:30:00.000Z"
}
```

5. Go to **locations** collection
6. Add a sample location:
```json
{
  "latitude": 13.0827,
  "longitude": 80.2707,
  "createdAt": "2025-12-25T15:30:00.000Z"
}
```

The map will automatically show this location with a marker!

7. Go to **device_status**
8. Add device info:
```json
{
  "deviceName": "Samsung A12",
  "isOnline": true,
  "battery": 85,
  "networkType": "WiFi",
  "createdAt": "2025-12-25T15:30:00.000Z"
}
```

9. Go to **call_recordings**
10. Add a recording entry:
```json
{
  "number": "+91-9876543210",
  "direction": "incoming",
  "duration": 125,
  "fileId": "recording_file_id_here",
  "createdAt": "2025-12-25T15:30:00.000Z"
}
```

### Step 5: Permissions Setup

Each collection needs proper permissions:

1. Click each collection → **Permissions**
2. Add these rules:
   - **Guest** → Read + List
   - **User** (your account) → All permissions

This allows the website to read data publicly.

### Step 6: Deploy & Test

1. Commit your updated `main.js` to GitHub
2. Netlify will auto-deploy
3. Go to https://boult.netlify.app
4. Enter password: **343421**
5. Click through sections:
   - **Calls** → See call logs
   - **Locations** → See interactive map with markers
   - **Device** → See device status cards
   - **Recordings** → See calls with download/delete buttons

## Features Explained

### Interactive Map
The **Locations** section uses **Leaflet.js** to show:
- World map centered on India
- Red markers for each location
- Click marker to see coordinates + timestamp
- Auto-fit map to show all locations
- Date filter to view specific dates

### Bulk Operations
All sections support:
- **Select all** → Check all rows
- **Deselect all** → Uncheck all rows
- **Delete selected** → Remove multiple entries
- **Date filter** → Filter by date range

### Call Recordings
The **Recordings** tab shows:
- Phone number
- Direction (Incoming/Outgoing)
- Duration in seconds
- Recording timestamp
- **Download** → Downloads from Appwrite Storage
- **Delete** → Removes from database

## Troubleshooting

### "Loading..." appears but no data shows
**Solution**: Check that your DATABASE_ID and COLLECTION_IDs are correct in `main.js`

### Map doesn't show
**Solution**: Make sure location documents have valid `latitude`/`longitude` numbers

### Download button doesn't work
**Solution**: Set up Appwrite Storage bucket and add real `fileId` values to recordings

### Changes don't appear on website
**Solution**: 
1. Make sure you committed changes to GitHub
2. Wait 1-2 minutes for Netlify to deploy
3. Hard refresh: `Ctrl+Shift+R` (or `Cmd+Shift+R` on Mac)

## Quick Recap

✅ **Website is deployed**: https://boult.netlify.app
✅ **All features are coded**: Maps, filters, bulk ops
✅ **All sections exist**: Calls, Locations, Device, Recordings
✅ **Need to do**: Configure Appwrite IDs in main.js

Once you add your Appwrite configuration, the dashboard will work perfectly!
