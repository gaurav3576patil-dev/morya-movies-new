MORYA MOVIE'S – नवीन Team Booking App
======================================

यात काय आहे
- Premium notebook-style interface आणि तुमचा MORYA LED SCREEN logo
- Marathi + English labels
- वर्षभराचा Calendar; एका तारखेला अनेक bookings
- ग्राहक, मोबाईल, तारीख, वेळ, location, event type, LED panels, Sq. Ft., screen size, notes, status
- Admin आणि Worker स्वतंत्र Login
- Admin आणि Worker दोघेही booking add/edit करू शकतात
- Delete फक्त Admin करू शकतो
- Payment (Total, Advance, Balance, Payment Note) वेगळ्या Firestore collection मध्ये; Worker ला Firestore rules ने access नाही
- दोन्ही फोनवर Firebase Cloud Sync

महत्त्वाचे
हा source project आहे. Firebase project/config आणि users तयार करेपर्यंत live login/sync चालणार नाही. Config placeholders आहेत. कोणताही password/OTP कुणालाही पाठवू नका.

सेटअप क्रम
1. https://console.firebase.google.com/ उघडा; Add project > MORYA MOVIE'S.
2. Build > Authentication > Get started > Email/Password enable करा.
3. Authentication > Users मध्ये तुमचा Admin email/password user तयार करा. UID copy करा.
4. Project settings > General > Your apps > Web app add करा. Firebase config copy करून public/firebase-config.js मध्ये placeholders बदला. OWNER_UID मध्ये Admin UID टाका.
5. Build > Firestore Database > Create database करा.
6. firestore/firestore.rules मधील PASTE_ADMIN_UID तुमच्या Admin UID ने बदला आणि Firebase Console > Firestore > Rules मध्ये पूर्ण rules paste करून Publish करा.
7. Authentication > Users मधून प्रत्येक Worker साठी वेगळा email/password user तयार करा.
8. Firestore Data मध्ये staff नावाचा collection तयार करा. प्रत्येक Worker चा UID हा Document ID ठेवा; document मध्ये role = "staff" field ठेवा.
9. App public folder Firebase Hosting किंवा HTTPS hosting वर deploy करा. PWA असल्याने Android Chrome मधून Add to Home screen करा.

Data model
- bookings/{id}: customer, phone, eventDate, eventTime, location, eventType, panels, sqft, screenSize, status, notes
- bookingPayments/{id}: amount, advance, note (Admin only)
- staff/{uid}: role: "staff" (owner console setup)

टीप: Firebase config मधील API key हा client config असतो; खरी सुरक्षा Firestore Rules आहेत. Owner UID योग्य भरणे आणि rules Publish करणे अनिवार्य आहे. Worker खात्याने payment access तपासल्याशिवाय प्रत्यक्ष वापर सुरू करू नका.
