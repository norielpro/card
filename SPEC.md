# Digital Card - Specification

## 1. Project Overview

- **Name**: Digital Card
- **Type**: Single-page web application (Single HTML)
- **Core functionality**: Create elegant contact cards with customizable background, photo, contact info, social links, QR code for adding to contacts, VCard export, and sharing as HTML.
- **Target users**: Professionals who want a stylish digital business card

## 2. UI/UX Specification

### Layout Structure
- **Desktop**: Centered card (max 420px), responsive padding
- **Mobile**: Full-width card with safe-area padding
- **Sections**: 
  1. Header with edit/view toggle
  2. Card preview (hero with background + photo)
  3. Contact info
  4. Social links
  5. Action buttons (QR, VCard, Share)

### Visual Design

#### Color Palette (Material You inspired)
- `--md-sys-color-primary`: #1C4B5E (Deep teal)
- `--md-sys-color-on-primary`: #FFFFFF
- `--md-sys-color-secondary`: #4A636D
- `--md-sys-color-surface`: #FAFDFD
- `--md-sys-color-surface-variant`: #DBE4E6
- `--md-sys-color-on-surface`: #191C1D
- `--md-sys-color-on-surface-variant`: #3F484A
- `--md-sys-color-outline`: #6F797A

#### Typography
- **Font family**: "Outfit" (Google Fonts) - modern geometric sans
- **Headings**: 600 weight
- **Body**: 400 weight
- **Sizes**:
  - Name: 24px
  - Title: 14px
  - Contact: 14px
  - Buttons: 13px

#### Spacing
- Card padding: 24px
- Section gap: 16px
- Button gap: 12px

#### Visual Effects
- Card: 16px border-radius, subtle shadow (0 4px 24px rgba(0,0,0,0.08))
- Buttons: 12px border-radius, ripple effect on click
- Transitions: 200ms ease-out
- Photo: circular, 100px, 3px border matching primary

### Background Options (8 elegant choices)
1. **Lunar Night** - #0D1B2A → #1B263B gradient
2. **Sunset Blush** - #2D1B2E → #662D4B gradient
3. **Forest Dusk** - #1A2F1A → #2D4A2D gradient
4. **Ocean Depth** - #0A192F → #193853 gradient
5. **Dusty Rose** - #2D2225 → #4A383D gradient
6. **Slate Mist** - #1E2D2F → #2F3D40 gradient
7. **Warm Sand** - #2D2720 → #4A4035 gradient
8. **Classic White** - #FFFFFF solid

### Components

#### Edit Mode
- Form inputs with floating labels (Material style)
- Photo upload with crop preview
- Background picker (grid of 8 options)
- Save/Cancel buttons

#### Card Display
- Hero section with background + gradient overlay
- Circular photo centered
- Name + title
- Contact items (phone, email, website)
- Social icons row (WhatsApp, Instagram, LinkedIn, Twitter, GitHub, Telegram)
- Action buttons: "Guardar Contacto", "Mostrar QR", "Compartir HTML", "Editar"

#### QR Modal
- Full-screen overlay
- QR code (VCard embedded)
- "Cerrar" button

## 3. Functionality Specification

### Core Features

#### Contact Management
- Create/edit personal card
- Save to localStorage
- Load on page open if exists

#### Card Data Fields
- Photo (base64, max 500KB)
- Name (required)
- Title/Profession
- Phone
- Email
- Website
- Company
- 6 social links (WhatsApp, Instagram, LinkedIn, Twitter, GitHub, Telegram)

#### VCard Generation (3.0 format)
```
BEGIN:VCARD
VERSION:3.0
FN:Name
TITLE:Title
ORG:Company
TEL:Phone
EMAIL:Email
URL:Website
URL:social1...
...
PHOTO;ENCODING=b;TYPE=jpg:base64...
END:VCARD
```

#### QR Code
- Library: qrcode.js
- Content: VCard as plain text
- Size: 256x256

#### Share as HTML
- Generate self-contained HTML with embedded data
- Opens in any browser
- Download as .html file

### User Flows

1. **First visit**: Empty card → Edit mode prompts
2. **Create card**: Fill form → Save → View mode
3. **Edit card**: Click Edit → Modify → Save
4. **Show QR**: Click QR → Modal with QR
5. **Save contact**: Click save → Downloads .vcf
6. **Share HTML**: Click share → Downloads .html

### Edge Cases
- No photo: Show default avatar placeholder
- No name: Prevent save, show error
- Large photo: Compress to max 500KB
- Missing social: Hide that icon
- localStorage full: Alert user

## 4. Acceptance Criteria

- [ ] Card renders with all 8 background options
- [ ] Photo displays correctly (or placeholder)
- [ ] All contact fields show/hide appropriately
- [ ] Social icons link correctly (open in new tab)
- [ ] QR code generates and scans correctly
- [ ] VCard imports to phone contacts
- [ ] HTML export opens standalone in browser
- [ ] Data persists in localStorage
- [ ] Works on mobile Chrome/Safari
- [ ] Material Design 3 aesthetics