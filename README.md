Phase 1: Service Architecture & Request Flow
1. System Services
User Interface (Next.js): A multi-step, mobile-responsive form for families to input data.
Authentication (Supabase Auth):
Users: Simple OTP or mobile-based login (for tracking their 6-month progress).
Nutritionists: Secure login to access the dashboard.
Database (PostgreSQL via Supabase): To store family profiles, member health data, and dietary audit logs.
File Storage (Supabase Storage): To store images/PDFs of blood reports.
AI/Analysis Layer (Optional/Future): A service to flag "Deficiency vs. Food" patterns before the nutritionist sees them.
2. The Request Flow
Onboarding: Family Head fills out the Next.js form (Registration → Members -> Blood Data → Food Audit).
Submission:
The frontend validates data using Zod.
Images are uploaded to Supabase Storage.
The JSON data is sent via a Next.js Server Action to the PostgreSQL database.
Nutritionist Review: The nutritionist logs into the /admin dashboard. They see a "Queue" of new families.
Prescription/Replacement: The nutritionist reviews the "Current Plate" (e.g., Refined Oil) and selects "D2D Replacements" (e.g., Cold Pressed Mustard Oil).
The "Protocol": A 6-month plan is generated and made available to the user.
Phase 2: Database Schema (Supabase/Postgres)
We need three main tables:
families: Store head name, mobile, address, and overall budget.
members: Linked to family_id. Stores age, gender, health complaints, and blood values.
food_audits: Linked to family_id. Stores the narrative (English/Hindi) about daily meals and kitchen practices.
