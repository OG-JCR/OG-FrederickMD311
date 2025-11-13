# 311 Service Request Form - Documentation

## Table of Contents
1. [Overview](#overview)
2. [Key Features](#key-features)
3. [Technical Stack](#technical-stack)
4. [Getting Started](#getting-started)
5. [Configuration](#configuration)
6. [Form Features](#form-features)
7. [API Integration](#api-integration)
8. [Security](#security)
9. [Customization Guide](#customization-guide)
10. [Adding or Modifying Form Fields](#adding-or-modifying-form-fields)
11. [Troubleshooting](#troubleshooting)
12. [Browser Compatibility](#browser-compatibility)
13. [Support & Maintenance](#support--maintenance)

---

## Overview

This is a **311 Service Request Form** for the City of Frederick, Maryland. The form allows residents to submit service requests (e.g., potholes, street lights, graffiti) with location-based validation and multimedia attachments.

### What This Form Does:
- ✅ Collects service request details from residents
- ✅ Validates addresses within Frederick city boundaries using geofencing
- ✅ Displays an interactive map for location selection
- ✅ Supports photo/video attachments
- ✅ Integrates with backend API for request submission
- ✅ Provides real-time address autocomplete
- ✅ Includes Google reCAPTCHA v2 for spam protection

---

## Key Features

### 🗺️ **Interactive Map with Geofencing**
- **ESRI ArcGIS Integration**: Interactive map powered by ArcGIS Maps SDK for JavaScript v4.28
- **Address Autocomplete**: Real-time address suggestions as users type
- **Geofencing Validation**: Automatically validates if the selected location is within Frederick city limits
- **Visual Boundary**: Displays Frederick city boundary overlay on the map
- **Click-to-Select**: Users can click on the map to select a location
- **Reverse Geocoding**: Converts map coordinates to human-readable addresses

### 📝 **Multi-Step Form**
- **Step 1**: Report an Issue - Select issue category and provide details
- **Step 2**: Location Details - Enter address or select on map
- **Step 3**: Contact Information - Provide contact details for follow-up

### 📷 **Media Upload**
- Supports photo and video uploads (max 10MB per file)
- Drag-and-drop functionality
- File preview before submission
- Automatic file size validation

### 🔒 **Security Features**
- Google reCAPTCHA v2 integration
- Content Security Policy (CSP) headers
- AES-256 encryption for sensitive data
- Token-based API authentication

### 📱 **Responsive Design**
- Mobile-first design approach
- Works on all devices (desktop, tablet, mobile)
- Touch-friendly interface
- Adaptive layouts

---

## Technical Stack

### Frontend Technologies:
- **HTML5** - Structure and semantics
- **CSS3** - Styling with CSS custom properties (variables)
- **JavaScript (ES6+)** - Client-side logic
- **Bootstrap 5.3.2** - UI framework and responsive grid
- **Bootstrap Icons 1.11.2** - Icon library
- **Google Fonts (Inter)** - Typography

### APIs & Services:
- **ESRI ArcGIS Maps SDK for JavaScript v4.28**
  - Interactive mapping
  - Geocoding services
  - Reverse geocoding
  - Address suggestions
  
- **Google reCAPTCHA v2**
  - Spam protection
  - Bot prevention
  
- **Ignatius API** (https://api.ignatius.io)
  - Backend data storage (API endpoint only)
  - Request submission
  - Report generation
  - **Note:** Portal access is via apps.opengov.com

### Libraries:
- **CryptoJS** - Encryption for secure data transmission
- **jQuery** - DOM manipulation (if needed)

---

## Getting Started

### Prerequisites:
1. **Web Server** - Any HTTP server (Apache, Nginx, IIS, or even a local dev server)
2. **ESRI ArcGIS API Key** - For map and geocoding services
3. **Google reCAPTCHA Keys** - Site key and secret key
4. **Backend API Access** - Ignatius API credentials
5. **Modern Web Browser** - Chrome, Firefox, Safari, Edge (latest versions)

### Installation:

1. **Upload the file to your web server:**
   ```bash
   # Example: Copy to web server directory
   cp index.html /var/www/html/311-form/
   ```

2. **Configure SSL/HTTPS** (Required for reCAPTCHA and geolocation):
   - Ensure your domain has a valid SSL certificate
   - reCAPTCHA requires HTTPS for production use

3. **Test the form:**
   - Open in a browser: `https://yourdomain.com/311-form/index.html`
   - Verify map loads correctly
   - Test address autocomplete
   - Submit a test request

---

## Configuration

### Required API Keys & Credentials

#### 1. ESRI ArcGIS API Key (Line 3155)
```javascript
const ESRI_API_KEY = "YOUR_ESRI_API_KEY_HERE";
```

**How to get an ESRI API Key:**
1. Go to https://developers.arcgis.com/
2. Sign up for a free developer account
3. Create an API key in your dashboard
4. Enable the following services:
   - Basemap
   - Geocoding
   - Routing (optional)

**API Key Permissions Required:**
- Geocoding (for address search)
- Basemap (for map display)
- Routing (optional)

---

#### 2. Google reCAPTCHA Keys (Search for "reCAPTCHA")
```javascript
// In HTML (line ~38):
<script src="https://www.google.com/recaptcha/api.js?onload=onRecaptchaLoad&render=explicit"></script>

// In JavaScript (search for "6LcI"):
const RECAPTCHA_SITE_KEY = "YOUR_RECAPTCHA_SITE_KEY";
```

**How to get reCAPTCHA keys:**
1. Go to https://www.google.com/recaptcha/admin
2. Register a new site
3. Choose reCAPTCHA v2 ("I'm not a robot" Checkbox)
4. Add your domain(s)
5. Copy the Site Key and Secret Key

**Important Notes:**
- Site Key goes in the HTML (client-side)
- Secret Key is used for server-side verification (backend)
- For testing on localhost, add `localhost` to allowed domains

---

#### 3. Backend API Configuration (Lines 3197-3199)
```javascript
const SERVER_URL_PAGE = "https://api.ignatius.io";
const PUBLIC_REQUESTS_TABLEKEY = "msfxaraq3"; // Public Requests Table
const REQUEST_EAM_REPORT_REPORT_ID = "vygamxbq7"; // Request EAM Report
```

**To Configure:**
- Replace `SERVER_URL_PAGE` with your backend API URL (this is the API endpoint, not the portal URL)
- Update `PUBLIC_REQUESTS_TABLEKEY` with your table identifier (found in apps.opengov.com)
- Update `REQUEST_EAM_REPORT_REPORT_ID` with your report ID (found in apps.opengov.com)

**Note:** The portal for managing tables and configurations is accessed at **apps.opengov.com**, while `api.ignatius.io` is the API endpoint used by the form for data submission.

---

#### 4. AES Encryption Key (Line 3156)
```javascript
const aesKEY = "YOUR_SECURE_32_CHARACTER_KEY_HERE";
```

**Security Note:**
- ⚠️ **IMPORTANT:** Never share this key publicly or commit it to version control
- This key is used for client-side encryption of sensitive data
- Must match the key configured on your backend server
- Generate a strong, random 32-character key
- Rotate this key periodically (recommended: every 90 days)
- Store securely and limit access to authorized personnel only
- Consider using environment variables or a secure key management system for production

---

### Theme Customization (Lines 41-70)

The form uses CSS custom properties for easy theme customization:

```css
:root {
  --fred-primary: #004785;      /* Primary blue color */
  --fred-secondary: #003766;     /* Secondary darker blue */
  --fred-accent: #FFD700;        /* Accent gold color */
  --fred-bg: #f0f4f8;           /* Background color */
  --fred-text: #1f2d3d;         /* Text color */
  /* ... more variables ... */
}
```

**To change the color scheme:**
1. Update the color values in the `:root` section
2. All components will automatically use the new colors
3. No need to modify individual component styles

---

## Form Features

### 1. Address Autocomplete

**Location:** Service address input field

**How it works:**
1. User starts typing an address
2. After 3 characters, ESRI Suggest API provides suggestions
3. User selects from dropdown
4. Address is geocoded to coordinates
5. Location is validated against city boundaries
6. If valid, map updates with marker

**Configuration:**
- Search delay: 300ms (debounced)
- Min characters: 3
- Max suggestions: 8
- Geographic bias: Frederick, MD center coordinates

---

### 2. Geofencing Validation

**Purpose:** Ensures service requests are only accepted for locations within Frederick city limits.

**How it works:**
1. City boundary is defined in GeoJSON format (embedded in code)
2. When user selects a location (map click or address), coordinates are validated
3. Ray-casting algorithm determines if point is inside boundary polygon
4. If outside: Shows error modal and prevents submission
5. If inside: Allows form submission

**Boundary Data Location:**
Search for `FREDERICK_BOUNDARY` in the code (around line 3000+)

**To update boundary:**
1. Obtain new GeoJSON boundary file
2. Replace the `FREDERICK_BOUNDARY` constant
3. Ensure coordinates are in [longitude, latitude] format
4. Test by clicking locations on map

---

### 3. Interactive Map

**Features:**
- Pan and zoom
- Click to select location
- Address search bar
- Boundary overlay visualization
- Custom marker placement
- Reverse geocoding display

**Map Controls:**
- Zoom in/out buttons
- Scale bar (desktop only)
- Boundary legend (desktop only)
- Current location button (optional)

**Customization:**
- Default center: Frederick, MD coordinates
- Default zoom level: 12
- Zoom constraints: min 10, max 16
- Basemap: ESRI Streets

---

### 4. Media Upload

**Supported Formats:**
- Images: JPG, JPEG, PNG, GIF
- Videos: MP4, MOV, AVI
- Max file size: 10MB per file

**Features:**
- Drag and drop support
- File preview thumbnails
- Multiple file upload
- File size validation
- File type validation
- Remove uploaded files

**Configuration:**
Search for `file upload` or `MAX_FILE_SIZE` to adjust limits

---

### 5. Form Validation

**Client-Side Validation:**
- Required field checking
- Email format validation
- Phone number format validation
- Address validation (geofencing)
- File size validation
- reCAPTCHA verification

**Real-time Feedback:**
- Field turns red if invalid
- Error messages appear below fields
- Submit button disabled until form is valid

---

## API Integration

### Request Submission Flow:

```
1. User fills form
   ↓
2. Client-side validation
   ↓
3. reCAPTCHA verification
   ↓
4. Data encryption (sensitive fields)
   ↓
5. POST to Ignatius API
   ↓
6. API processes and stores request
   ↓
7. Success confirmation shown to user
```

### API Endpoints Used:

#### 1. Submit Service Request
```
POST https://api.ignatius.io/api/tableRecords
Headers:
  - Content-Type: application/json
  - Authorization: Bearer {token}
Body:
  - tableKey: "msfxaraq3"
  - recordValues: { /* form data */ }
```

#### 2. ESRI Geocoding API
```
GET https://geocode-api.arcgis.com/arcgis/rest/services/World/GeocodeServer/findAddressCandidates
Parameters:
  - token: {ESRI_API_KEY}
  - Single Line Input: {address}
  - f: json
```

#### 3. ESRI Suggest API (Autocomplete)
```
GET https://geocode-api.arcgis.com/arcgis/rest/services/World/GeocodeServer/suggest
Parameters:
  - token: {ESRI_API_KEY}
  - text: {user input}
  - f: json
```

---

## Security

### Content Security Policy (CSP)

The form includes strict CSP headers (lines 8-18):

```html
<meta http-equiv="Content-Security-Policy" content="
  default-src 'self';
  connect-src 'self' https://*.arcgis.com https://*.esri.com ...;
  script-src 'self' 'unsafe-inline' 'unsafe-eval' ...;
  ...
" />
```

**Purpose:**
- Prevents XSS (Cross-Site Scripting) attacks
- Restricts resource loading to trusted sources
- Mitigates code injection vulnerabilities

**To modify CSP:**
- Add new domains to appropriate directives
- Be cautious with 'unsafe-inline' and 'unsafe-eval'
- Test thoroughly after changes

---

### Data Encryption

**AES-256 Encryption:**
- Sensitive form data is encrypted before transmission
- Uses CryptoJS library
- Encryption key must match backend key

**Encrypted Fields:**
- Contact information
- Personal details
- Request descriptions (optional)

---

### reCAPTCHA Protection

**Configuration:**
1. Embedded on form (explicit rendering)
2. Required before form submission
3. Verifies user is human, not bot
4. Score-based validation (v2 checkbox)

**Implementation:**
- JavaScript callback: `onRecaptchaLoad()`
- Validation: `enableSubmitButton()` called when verified
- Reset on submission

---

## Customization Guide

### 1. Change Form Title and Header

**Line 2059:**
```html
<h1 class="header-title">
  <i class="bi bi-building-check me-2"></i>
  Submit 311 Service Request
</h1>
```

**To change:**
- Update the text "Submit 311 Service Request"
- Change icon by replacing `bi-building-check` with another Bootstrap Icon

---

### 2. Modify Issue Categories

**Search for:** "Issue Type Selector" or category dropdown

**Example:**
```javascript
const categories = [
  { value: "pothole", label: "Pothole" },
  { value: "streetlight", label: "Street Light Out" },
  { value: "graffiti", label: "Graffiti" },
  // Add more categories here
];
```

---

### 3. Adjust Map Settings

**Location:** Search for `FREDERICK_CENTER` and `FREDERICK_ZOOM`

```javascript
const FREDERICK_CENTER = [-77.4106, 39.4143]; // [longitude, latitude]
const FREDERICK_ZOOM = 12;
```

**To change:**
- Replace with your city's coordinates
- Adjust zoom level (10-16 recommended)

---

### 4. Update Contact Information

**Search for:** Footer section or "More Information"

```html
<div class="footer-info-item">
  <strong>Phone:</strong>
  <a href="tel:+13016003900">+1 (301) 600-3900</a>
</div>
```

---

### 5. Modify Color Scheme

**Line 41-70:** CSS Custom Properties

```css
:root {
  --fred-primary: #004785;  /* Change to your primary color */
  --fred-accent: #FFD700;   /* Change to your accent color */
  /* ... more colors ... */
}
```

---

### 6. Enable/Disable Features

**Disable reCAPTCHA for testing:**
```javascript
// Comment out reCAPTCHA requirement:
// enableSubmitButton(); // Remove condition
```

**Disable geofencing:**
```javascript
function isPointInFrederick(latitude, longitude) {
  return true; // Always allow (for testing)
}
```

---

## Troubleshooting

### Common Issues:

#### 1. Map Not Loading
**Symptoms:** Gray box instead of map

**Solutions:**
- Check ESRI API key is valid and active
- Verify API key has correct permissions (Basemap, Geocoding)
- Check browser console for errors
- Ensure `https://` is used (not `http://`)
- Verify CSP allows ESRI domains

---

#### 2. Address Autocomplete Not Working
**Symptoms:** No suggestions appear when typing

**Solutions:**
- Verify ESRI API key has Geocoding service enabled
- Check network tab for API errors (401 Unauthorized, 429 Rate Limit)
- Ensure minimum 3 characters are typed
- Check `ESRI_API_KEY` variable is set correctly

---

#### 3. Form Submission Fails
**Symptoms:** Error message after clicking submit

**Solutions:**
- Check backend API is accessible (`SERVER_URL_PAGE`)
- Verify API credentials (`tableKey`, `reportId`)
- Check browser console for detailed error
- Ensure reCAPTCHA is completed
- Verify all required fields are filled

---

#### 4. reCAPTCHA Not Appearing
**Symptoms:** No reCAPTCHA checkbox visible

**Solutions:**
- Check reCAPTCHA site key is correct
- Verify domain is registered in reCAPTCHA admin
- Ensure JavaScript is enabled in browser
- Check for CSP blocking (`frame-src` directive)
- Test on HTTPS (reCAPTCHA requires HTTPS for production)

---

#### 5. Location Outside Boundary Error
**Symptoms:** "Location outside service area" modal appears for valid addresses

**Solutions:**
- Verify boundary GeoJSON data is correct
- Check coordinate format ([longitude, latitude], not [lat, lng])
- Test with known valid address
- Review `isPointInFrederick()` function logic
- Check if boundary data is properly loaded

---

#### 6. File Upload Issues
**Symptoms:** Cannot upload photos/videos

**Solutions:**
- Check file size (must be < 10MB)
- Verify file format (JPG, PNG, MP4, etc.)
- Ensure sufficient browser storage
- Check browser console for errors
- Test with different file

---

### Debug Mode

**Enable console logging:**
1. Open browser Developer Tools (F12)
2. Go to Console tab
3. Look for error messages in red
4. Check Network tab for failed API calls

**Add debug logging:**
```javascript
// Add at various points in code:
console.log('Debug:', variableName);
console.error('Error:', error);
```

---

## Browser Compatibility

### Supported Browsers:
- ✅ Chrome 90+ (Recommended)
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+
- ✅ Mobile browsers (iOS Safari, Chrome Mobile)

### Known Issues:
- **Internet Explorer:** Not supported (uses modern JavaScript features)
- **Safari < 14:** May have geocoding issues
- **Firefox:** Ensure CSP compatibility

### Testing Checklist:
- [ ] Map loads correctly
- [ ] Address autocomplete works
- [ ] Form submits successfully
- [ ] File uploads work
- [ ] reCAPTCHA displays and validates
- [ ] Responsive on mobile devices
- [ ] All buttons clickable
- [ ] Error messages display correctly

---

## Support & Maintenance

### Regular Maintenance Tasks:

#### Monthly:
- [ ] Monitor ESRI API usage (check quota)
- [ ] Review form submissions for errors
- [ ] Check for broken links
- [ ] Test reCAPTCHA functionality

#### Quarterly:
- [ ] Update ESRI API library version (if needed)
- [ ] Review and update boundary data
- [ ] Check for Bootstrap/library updates
- [ ] Audit CSP policy

#### Annually:
- [ ] Rotate encryption keys
- [ ] Renew SSL certificate
- [ ] Review and update security policies
- [ ] Update issue categories if needed

---

### Performance Optimization:

**Tips for faster loading:**
1. Enable server-side compression (gzip)
2. Use CDN for libraries (already implemented)
3. Optimize images before upload
4. Enable browser caching
5. Minify HTML/CSS/JS for production

**Current optimizations:**
- ✅ CDN-hosted libraries (Bootstrap, Icons, Fonts)
- ✅ Debounced address search (300ms)
- ✅ Lazy map initialization
- ✅ Conditional mobile features

---

### Monitoring:

**Metrics to track:**
- Form submission success rate
- Average time to complete form
- Map loading time
- API error rates
- ESRI API quota usage
- reCAPTCHA success rate

**Tools:**
- Google Analytics (optional)
- Server access logs
- ESRI API dashboard
- reCAPTCHA admin console

---

### Getting Help:

**Documentation:**
- ESRI ArcGIS: https://developers.arcgis.com/javascript/
- Bootstrap: https://getbootstrap.com/docs/
- reCAPTCHA: https://developers.google.com/recaptcha/docs/

**Support Contacts:**
- **Technical Support:** [Your support email/phone]
- **ESRI Support:** https://support.esri.com/
- **Google reCAPTCHA:** https://support.google.com/recaptcha/

---

## Version History

### Version 1.0 (Current)
- Initial release with full functionality
- ESRI ArcGIS map integration
- Address autocomplete with geofencing
- Multi-step form with validation
- Media upload support
- reCAPTCHA v2 integration
- Responsive mobile-first design

---

## License & Credits

### Third-Party Services:
- **ESRI ArcGIS** - Mapping and geocoding services
- **Google reCAPTCHA** - Spam protection
- **Bootstrap** - UI framework
- **Bootstrap Icons** - Icon library
- **Google Fonts** - Typography (Inter font family)

### Credits:
- Developed for: City of Frederick, Maryland
- Form Type: 311 Service Request System
- API Backend: Ignatius Platform

---

## Quick Reference

### Important Code Locations:

| Feature | Search Term | Approximate Line |
|---------|-------------|------------------|
| ESRI API Key | `ESRI_API_KEY` | 3155 |
| Server URL | `SERVER_URL_PAGE` | 3197 |
| Map Center | `FREDERICK_CENTER` | ~3200 |
| Boundary Data | `FREDERICK_BOUNDARY` | ~3220 |
| reCAPTCHA Config | `reCAPTCHA` or `onRecaptchaLoad` | ~3500 |
| Form Submission | `submitForm` | ~6000 |
| Address Autocomplete | `initializeAddressAutocomplete` | ~5370 |
| Geofencing Logic | `isPointInFrederick` | ~3524 |
| Theme Colors | `:root` CSS variables | 41-70 |

---

## Adding or Modifying Form Fields

This section provides step-by-step instructions for technical users who need to add new fields or modify existing fields in the 311 Service Request Form.

### Overview: Form Data Flow

Understanding how data flows through the system is critical before making changes:

```
User Input (HTML Form)
    ↓
JavaScript Collection (FormData)
    ↓
Service Request Data Object
    ↓
API Payload (fieldsList array)
    ↓
GAB Database (Public Requests Table)
    ↓
Webhook Integration
    ↓
EAM System
```

**Important:** Field names must match exactly across all systems (Form → GAB → EAM) for the integration to work properly.

---

### Prerequisites Checklist

Before adding or modifying fields, verify the following:

#### 1. **Does the field exist in EAM?**
- [ ] Log into your EAM system
- [ ] Navigate to the relevant work order or asset module
- [ ] Verify the field name (exact spelling and capitalization matter)
- [ ] Note if the field is:
  - Free text (input field)
  - Dropdown list (select field)
  - Date/time field
  - Number field
  - Boolean (Yes/No)

#### 2. **Does the field exist in GAB (Ignatius)?**
- [ ] Log into GAB (apps.opengov.com)
- [ ] Navigate to the **Public Requests** table
- [ ] Check if the field exists in the table schema
- [ ] Verify the field name matches EAM exactly
- [ ] Note the field type (Text, Number, Date, Boolean, etc.)

**If the field doesn't exist in GAB:**
1. Go to Table Settings → Add New Field
2. Use the **exact same name** as in EAM
3. Select the appropriate field type
4. Save the table schema

#### 3. **If it's a dropdown field, do the values match?**
- [ ] Compare dropdown options in EAM
- [ ] Verify dropdown options in GAB match exactly
- [ ] Ensure spelling, capitalization, and punctuation are identical

**Example:**
- ✅ Good: "Yes" in form, "Yes" in GAB, "Yes" in EAM
- ❌ Bad: "Yes" in form, "yes" in GAB, "YES" in EAM

#### 4. **Update the GAB → EAM Webhook**
- [ ] Log into GAB
- [ ] Navigate to **Public Requests** table
- [ ] Click **Automations** tab
- [ ] Click **Webhooks**
- [ ] Edit the existing **GAB → EAM** integration webhook
- [ ] Update the payload mapping to include your new field
- [ ] Test the webhook with sample data

---

### Step-by-Step: Adding a New Field

Follow these steps to add a completely new field to the form.

#### **Step 1: Add the HTML Form Field**

Locate where you want to add the field in `index.html`. Fields are organized by step:
- **Step 1** (lines ~2050-2200): Service type selection
- **Step 2** (lines ~2400-2850): Location and additional details

**Example: Adding a "Priority Level" dropdown field**

Search for similar fields in the HTML (e.g., search for `<select` to find dropdown examples).

Add your new field:

```html
<!-- Priority Level Field -->
<div class="form-group mb-3">
  <label for="priorityLevel" class="form-label">
    Priority Level <span class="required">*</span>
  </label>
  <select id="priorityLevel" name="priorityLevel" class="form-control form-select" required>
    <option value="">Select priority...</option>
    <option value="Low">Low</option>
    <option value="Medium">Medium</option>
    <option value="High">High</option>
    <option value="Critical">Critical</option>
  </select>
  <div class="form-help">
    Select the urgency level for this request
  </div>
</div>
```

**Key Points:**
- `id` and `name` attributes should match your GAB/EAM field name (use camelCase for JavaScript, but this will be mapped later)
- Use `class="form-control"` for text inputs
- Use `class="form-control form-select"` for dropdowns
- Add `required` attribute if the field is mandatory
- Dropdown `<option value="">` must match GAB/EAM values exactly

---

#### **Step 2: Collect the Field Value in JavaScript**

Find the form submission handler (search for `form.addEventListener("submit"` around line 6635).

The form automatically collects all fields via `FormData`, but you need to add it to the `serviceRequestData` object.

**For fields that apply to ALL request types:**

Find the `serviceRequestData` object creation (around line 6708) and add your field:

```javascript
const serviceRequestData = {
  requestInfo: {
    requestType: formData.get("requestType"),
    status: "Open",
    submissionTime: new Date().toISOString(),
    isAnonymous: true,
    priorityLevel: formData.get("priorityLevel") || ""  // ADD THIS LINE
  },
  // ... rest of the object
};
```

**For fields specific to certain request types:**

Find the `additionalInfo` section (around line 6725):

```javascript
additionalInfo: {
  lidDamage: formData.get("lidDamage") || "",
  toterBodyDamage: formData.get("toterBodyDamage") || "",
  // ... existing fields ...
  priorityLevel: formData.get("priorityLevel") || "",  // ADD THIS LINE
  // ... more fields
}
```

---

#### **Step 3: Add Field to API Payload**

Find the `createServiceRequest` function (search for `async function createServiceRequest` around line 3809).

Add your field to the `fieldsList` array:

```javascript
const fieldsList = [
  {
    Name: "request_category",
    Value: serviceRequestData.requestInfo.requestType
  },
  // ... existing fields ...
  {
    Name: "priority_level",  // USE THE EXACT GAB/EAM FIELD NAME
    Value: serviceRequestData.requestInfo.priorityLevel || ""
  },
  // ... more fields
];
```

**Critical:** The `Name` property must match the exact field name in GAB and EAM. Use underscores (snake_case) as this is the typical database convention.

**For conditional fields (only for specific request types):**

Find the conditional logic (around line 3854) and add your field:

```javascript
if (serviceRequestData.requestInfo.requestType === 'Bin Request - Repair/Replace') {
  fieldsList.push({
    Name: "lid_damage_only",
    Value: serviceRequestData.additionalInfo.lidDamage || ""
  });
  
  // ADD YOUR NEW FIELD HERE
  fieldsList.push({
    Name: "priority_level",
    Value: serviceRequestData.additionalInfo.priorityLevel || ""
  });
  
  // ... more fields
}
```

---

#### **Step 4: Update the GAB → EAM Webhook Payload**

This is the most critical step for the integration to work.

1. **Log into GAB** (apps.opengov.com)
2. Navigate to **Public Requests** table
3. Click **Automations** tab → **Webhooks**
4. Edit the **GAB → EAM Integration** webhook
5. Update the payload mapping:

```json
{
  "WorkOrderNumber": "{{request_id}}",
  "RequestCategory": "{{request_category}}",
  "Description": "{{description}}",
  "PriorityLevel": "{{priority_level}}",
  "Latitude": "{{latitude}}",
  "Longitude": "{{longitude}}"
}
```

**Important Notes:**
- Use `{{field_name}}` syntax to reference GAB fields
- The left side (e.g., `"PriorityLevel"`) is the EAM field name
- The right side (e.g., `"{{priority_level}}"`) is the GAB field name
- Field names must match exactly (case-sensitive)

6. **Test the webhook** with sample data
7. **Save** the webhook configuration

---

### Step-by-Step: Modifying an Existing Field

#### **Adding a New Dropdown Option**

If you need to add a new option to an existing dropdown field:

**Step 1: Update the HTML**

Find the dropdown field in `index.html` (search for the field's `id`):

```html
<select id="toterSize" name="toterSize" class="form-control">
  <option value="">Select size...</option>
  <option value="64 Gallon">64 Gallon</option>
  <option value="96 Gallon">96 Gallon</option>
  <option value="128 Gallon">128 Gallon</option>  <!-- ADD NEW OPTION -->
</select>
```

**Step 2: Update GAB Field**

1. Log into GAB
2. Go to **Public Requests** table → **Table Settings**
3. Find the field (e.g., `toter_size`)
4. If it's a dropdown type, add the new option: `128 Gallon`
5. Save changes

**Step 3: Update EAM Field**

1. Log into EAM
2. Navigate to the corresponding field
3. Add the same option: `128 Gallon`
4. Save changes

**Step 4: Test the Integration**

1. Submit a test form with the new option
2. Verify it appears correctly in GAB
3. Check that the webhook sends it to EAM successfully
4. Confirm EAM accepts the value without errors

---

#### **Commenting Out (Hiding) a Field**

To temporarily disable a field without deleting it:

**Step 1: Comment out the HTML**

Find the field in `index.html` and wrap it in HTML comments:

```html
<!-- DISABLED: Priority Level Field
<div class="form-group mb-3">
  <label for="priorityLevel" class="form-label">
    Priority Level <span class="required">*</span>
  </label>
  <select id="priorityLevel" name="priorityLevel" class="form-control form-select" required>
    <option value="">Select priority...</option>
    <option value="Low">Low</option>
    <option value="Medium">Medium</option>
  </select>
</div>
-->
```

**Step 2: Remove from JavaScript (Optional)**

If you want to completely stop sending the field:

Find the field in the `serviceRequestData` object and comment it out:

```javascript
additionalInfo: {
  lidDamage: formData.get("lidDamage") || "",
  // priorityLevel: formData.get("priorityLevel") || "",  // DISABLED
  toterBodyDamage: formData.get("toterBodyDamage") || "",
}
```

Find the field in the `fieldsList` array and comment it out:

```javascript
// DISABLED: Priority Level
// fieldsList.push({
//   Name: "priority_level",
//   Value: serviceRequestData.additionalInfo.priorityLevel || ""
// });
```

**Step 3: Update GAB Webhook (Optional)**

If the field is no longer being sent, you can remove it from the webhook payload mapping (but it's safe to leave it - it will just send an empty value).

---

### Common Field Types and Examples

#### **Text Input Field**

```html
<div class="form-group mb-3">
  <label for="fieldName" class="form-label">
    Field Label <span class="required">*</span>
  </label>
  <input
    type="text"
    id="fieldName"
    name="fieldName"
    class="form-control"
    placeholder="Enter text here..."
    required
  />
</div>
```

#### **Textarea (Multi-line Text)**

```html
<div class="form-group mb-3">
  <label for="fieldName" class="form-label">
    Field Label <span class="required">*</span>
  </label>
  <textarea
    id="fieldName"
    name="fieldName"
    class="form-control"
    rows="4"
    placeholder="Enter detailed description..."
    required
  ></textarea>
</div>
```

#### **Dropdown (Select) Field**

```html
<div class="form-group mb-3">
  <label for="fieldName" class="form-label">
    Field Label <span class="required">*</span>
  </label>
  <select id="fieldName" name="fieldName" class="form-control form-select" required>
    <option value="">Select an option...</option>
    <option value="Option 1">Option 1</option>
    <option value="Option 2">Option 2</option>
    <option value="Option 3">Option 3</option>
  </select>
</div>
```

#### **Number Input Field**

```html
<div class="form-group mb-3">
  <label for="fieldName" class="form-label">
    Field Label <span class="required">*</span>
  </label>
  <input
    type="number"
    id="fieldName"
    name="fieldName"
    class="form-control"
    min="0"
    max="100"
    placeholder="Enter number..."
    required
  />
</div>
```

#### **Date/Time Field**

```html
<div class="form-group mb-3">
  <label for="fieldName" class="form-label">
    Field Label <span class="required">*</span>
  </label>
  <input
    type="datetime-local"
    id="fieldName"
    name="fieldName"
    class="form-control"
    required
  />
</div>
```

---

### Field Naming Conventions

To maintain consistency across systems, follow these naming conventions:

| Context | Convention | Example |
|---------|-----------|---------|
| HTML `id` and `name` | camelCase | `priorityLevel` |
| JavaScript variable | camelCase | `priorityLevel` |
| GAB/EAM field name | snake_case | `priority_level` |
| API payload `Name` | snake_case | `priority_level` |
| Webhook mapping | snake_case | `{{priority_level}}` |

**Example Mapping:**

```
HTML: <input id="priorityLevel" name="priorityLevel">
  ↓
JavaScript: formData.get("priorityLevel")
  ↓
API Payload: Name: "priority_level"
  ↓
GAB Field: priority_level
  ↓
EAM Field: priority_level
```

---

### Testing Your Changes

After making changes, follow this testing checklist:

#### **1. Local Testing**
- [ ] Open the form in a browser
- [ ] Verify the new field appears correctly
- [ ] Test form validation (required fields, etc.)
- [ ] Check browser console for JavaScript errors (F12 → Console)

#### **2. Submission Testing**
- [ ] Fill out the form completely
- [ ] Submit a test request
- [ ] Verify success message appears
- [ ] Check browser console for errors

#### **3. GAB Verification**
- [ ] Log into GAB
- [ ] Navigate to **Public Requests** table
- [ ] Find your test submission
- [ ] Verify the new field value was saved correctly
- [ ] Check that the value matches what you entered

#### **4. EAM Integration Testing**
- [ ] Log into EAM
- [ ] Find the work order created from your test submission
- [ ] Verify the new field value appears in EAM
- [ ] Confirm the value matches GAB and your form input
- [ ] Check for any error logs in the webhook history

#### **5. Edge Case Testing**
- [ ] Test with empty/optional fields
- [ ] Test with maximum length values
- [ ] Test with special characters (if applicable)
- [ ] Test dropdown options one by one
- [ ] Test form submission without the new field (if optional)

---

### Troubleshooting

#### **Field value not appearing in GAB**

**Possible causes:**
1. Field name mismatch between HTML and JavaScript
2. Field not added to `serviceRequestData` object
3. Field not added to `fieldsList` array
4. GAB field doesn't exist or has wrong name

**Solution:**
- Check browser console for errors
- Verify field names match exactly (case-sensitive)
- Confirm field exists in GAB table schema

---

#### **Field value not appearing in EAM**

**Possible causes:**
1. Webhook payload not updated
2. Field name mismatch between GAB and EAM
3. EAM field doesn't accept the value format
4. Webhook is failing (check logs)

**Solution:**
- Check webhook execution logs in GAB
- Verify field names match in GAB and EAM
- Test webhook with sample data
- Check EAM error logs

---

#### **Dropdown value rejected by EAM**

**Possible causes:**
1. Dropdown option doesn't exist in EAM
2. Spelling/capitalization mismatch
3. Extra spaces in the value

**Solution:**
- Compare dropdown options character-by-character
- Ensure exact match (case-sensitive)
- Remove any leading/trailing spaces
- Add the option to EAM if missing

---

#### **Form validation not working**

**Possible causes:**
1. Missing `required` attribute in HTML
2. Field not included in validation logic
3. JavaScript error preventing validation

**Solution:**
- Add `required` attribute to HTML field
- Check browser console for errors
- Verify field is included in `requiredFields` array (if applicable)

---

### Quick Reference: Key Code Locations

| What You Need | Where to Find It | Approximate Line |
|---------------|------------------|------------------|
| Step 1 HTML fields | Search for "Step 1" or service categories | 2050-2200 |
| Step 2 HTML fields | Search for "Step 2" or location section | 2400-2850 |
| Additional info fields | Search for "additionalInfoSection" | 2500-2850 |
| Form submission handler | Search for `form.addEventListener("submit"` | 6635 |
| Service request data object | Inside form submit handler | 6708-6745 |
| Create service request function | Search for `async function createServiceRequest` | 3809 |
| Field list array | Inside `createServiceRequest` function | 3819-3851 |
| Conditional fields logic | Inside `createServiceRequest` function | 3854-3932 |

---

### Best Practices

1. **Always test in a test script first** before deploying to production
2. **Document your changes** in code comments
3. **Use descriptive field names** that clearly indicate the field's purpose
4. **Keep field names consistent** across all systems (Form, GAB, EAM)
5. **Validate user input** on both client-side (HTML/JavaScript) and server-side (GAB/EAM)
6. **Provide helpful placeholder text** and form help text for users
7. **Test the complete integration** from form submission to EAM work order creation
8. **Keep a backup** of the working form before making major changes
9. **Use version control** (Git) to track changes
10. **Communicate changes** to your team and update documentation

---

### Getting Help

If you encounter issues or need assistance:

1. **Check browser console** (F12 → Console) for JavaScript errors
2. **Review GAB webhook logs** for integration errors
3. **Check EAM error logs** for rejected values
4. **Verify field names** match exactly across all systems
5. **Test with simple values** first (e.g., "Test" instead of complex text)
6. **Contact your technical support team** with specific error messages

---

## Conclusion

This form provides a complete, production-ready solution for collecting 311 service requests with advanced geospatial features. For questions or support, please contact your technical support team.

**Thank you for using this service request form!**

---

**Last Updated:** November 2024  
**Document Version:** 2.0  
**Form Version:** 1.0
