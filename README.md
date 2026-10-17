# BHARTH SHOP

Mobile-first product catalog with a React/Vite storefront, Express/MongoDB API, local image storage, and protected admin catalog tools.

## Requirements

- Node.js 20+
- MongoDB running locally or a MongoDB connection string

## Setup

1. Copy `backend/.env.example` to `backend/.env` and set `MONGODB_URI`, a long random `JWT_SECRET`, and initial admin email/password.
2. Install dependencies from the repository root: `npm install`, `npm install --prefix frontend`, and `npm install --prefix backend`.
3. Create/update the initial admin account: `npm run create-admin --prefix backend`.
4. Start both apps: `npm run dev`.
5. Open `http://localhost:5173`. API runs on `http://localhost:5000`.

Frontend and backend can also run independently with `npm run dev --prefix frontend` and `npm run dev --prefix backend`. For a split deployment, set the frontend build variable `VITE_API_URL` to the backend's public origin (for example, `https://api.example.com`) and set backend `FRONTEND_URL` to the frontend's public origin. The same backend origin is used to resolve stored relative image paths.

## Manual workflow checklist

- Sign in at `/admin` with the account created by the setup script.
- Add a product with an image, edit its fields/stock or replace its image, then delete it.
- Verify the customer listing, search, stock display, and product detail page reflect the saved values.
- Open admin endpoints while signed out and confirm writes return HTTP 401.
- Check the storefront at 320px, 360px, 390px, and desktop widths.

Product images are stored in `backend/uploads/products` by default, independent of the server's startup directory. MongoDB stores relative image URLs. On hosts with ephemeral filesystems, attach persistent storage and set backend `UPLOAD_DIR` to its mounted directory; otherwise uploaded files can disappear on redeploy and their image URLs will return 404. Copy existing uploads to the persistent directory when migrating. Admin authentication uses expiring signed JWTs held in session storage and passwords are bcrypt hashed.
