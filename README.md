Build "PayPool", a mobile-first Indian UPI Expense & Split-Bill Tracker with AI Receipt OCR.

### Connected Apps & Architecture
- **Frontend:** React, Vite, Tailwind CSS, Lucide Icons, and `qrcode.react` for UPI QR codes.
- **Backend & Database:** Connect **Lovable Cloud** (or Supabase) for Email/Google Authentication, Storage bucket (`receipts`) for uploaded bill photos, and PostgreSQL tables (`bills`, `bill_items`, `participants`) with Row-Level Security.
- **Receipt OCR Integration:** Create a backend Edge Function (`scan-receipt`) connected to **Lovable AI** (or Google Gemini API via `GEMINI_API_KEY` secret) that accepts an uploaded receipt image and returns structured JSON:
  `{ merchant_name, date, items: [{ name, qty, price }], cgst, sgst, service_charge, grand_total }`.

### Core Features
1. **Branding & Navigation:**
   - Display the **PayPool** logo and clean fintech UI across the header, browser page title, and dashboard.

2. **Receipt Upload & Editable Review Table:**
   - Upload JPG/PNG photos of restaurant bills or Kirana receipts to storage and trigger `scan-receipt`.
   - Show an editable table where the user can fix misread item names/prices, add/delete items, or adjust GST before splitting.

3. **Equal & Itemized Bill Splitter:**
   - Add friends with Name and optional UPI ID (e.g., `rahul@okicici`).
   - **Equal Split:** Divide the grand total equally among selected friends.
   - **Itemized Split:** Assign specific items to one or more friends, automatically distributing CGST/SGST and service charges proportionally based on each person's item subtotal.

4. **NPCI UPI Payment Links & QR Codes:**
   - Generate standard UPI links for each friend's share:
     `upi://pay?pa=<PAYER_UPI_ID>&pn=<PAYER_NAME>&am=<AMOUNT_2_DECIMALS>&cu=INR&tn=PayPool_<BILL_NOTE>`
   - Render a scannable QR code (`qrcode.react`) for desktop users, a direct **"Pay via UPI App"** button for mobile users, and a **"Copy WhatsApp Split Summary"** button branded with PayPool.

5. **Expense Dashboard & Settlement Tracking:**
   - Include a manual **"Mark as Paid / Pending"** toggle for each participant to track who has settled their share.
   - Show a clean summary dashboard with total monthly spend (in ₹), category breakdown (Food, Groceries, Travel, Utilities), and recent split history.

