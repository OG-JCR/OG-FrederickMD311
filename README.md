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
10. [Troubleshooting](#troubleshooting)
11. [Browser Compatibility](#browser-compatibility)
12. [Support & Maintenance](#support--maintenance)

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
  - Backend data storage
  - Request submission
  - Report generation

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
- Replace `SERVER_URL_PAGE` with your backend API URL
- Update `PUBLIC_REQUESTS_TABLEKEY` with your table identifier
- Update `REQUEST_EAM_REPORT_REPORT_ID` with your report ID

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

## Conclusion

This form provides a complete, production-ready solution for collecting 311 service requests with advanced geospatial features. For questions or support, please contact your technical support team.

**Thank you for using this service request form!**

---

**Last Updated:** November 2024  
**Document Version:** 1.0  
**Form Version:** 1.0
