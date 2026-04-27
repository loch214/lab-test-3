# 🚀 MERN Stack Enhancement & Deployment Guide

---

## Phase 1: Local Environment Setup

1. **Install Node.js & NPM** — Download the LTS version from [nodejs.org](https://nodejs.org/)
2. **Initialize Project**
   - Run `npm install` inside the `backend` folder
   - Run `npm install` inside the `frontend` folder
3. **Database** — Create a cluster on [MongoDB Atlas](https://www.mongodb.com/cloud/atlas), allow access from `0.0.0.0/0`, and copy your Connection String

---

## Phase 2: Feature Enhancement

To add new attributes (e.g., Stock and Discount Percentage):

### 1. Backend Update

- **File:** `backend/models/Item.js`
- **Action:** Add the new fields to the Mongoose Schema

```js
stock: { type: Number, required: true },
discountPercentage: { type: Number, default: 0 }
```

### 2. Frontend Update — The Form

- **File:** `frontend/src/pages/ItemForm.jsx`
- **Action:**
  - Add `<input>` tags for the new fields
  - Ensure the `name` attribute matches the Schema field name
  - Ensure the state is updated inside `handleChange`

### 3. Frontend Update — The Display

- **File:** `frontend/src/components/ItemCard.jsx`
- **Action:** Add JSX to display `item.stock` and `item.discountPercentage`

---

## Phase 3: Backend Deployment (Render)

1. **Create Web Service** — Connect your GitHub repo to [Render](https://render.com/)
2. **Root Directory** — Set to `backend`
3. **Build Command** — `npm install`
4. **Start Command** — `node server.js`
5. **Environment Variables** — Add `MONGO_URI` with your Atlas connection string
6. **CORS Fix** — In `server.js`, add the following **before** your routes:

```js
app.use(cors());
```

---

## Phase 4: Frontend Deployment (Vercel)

1. **Create Project** — Import your GitHub repo to [Vercel](https://vercel.com/)
2. **Framework Preset** — Select `Vite`
3. **Root Directory** — Set to `frontend`
4. **Build Settings**

   | Setting | Value |
   |---|---|
   | Build Command | `npm run build` |
   | Output Directory | `dist` |
   | Install Command | `npm install` |

5. **Environment Variables**

   | Key | Value |
   |---|---|
   | `VITE_API_URL` | `https://your-backend-url.onrender.com/api` |

6. **Redeploy** — If you update the backend URL, click **Redeploy** on the Vercel dashboard

---

## Phase 5: Verification

- **Network Tab (F12)** — Confirm requests go to your Render URL, not `localhost`
- **CORS Check** — No red `CORS Policy` errors in the browser console
- **Persistence** — Add an item and refresh the page; if it stays, MongoDB is connected correctly

---

## 💡 Pro Tips

- **Case Sensitivity** — `name` attributes in the frontend form must exactly match the backend Schema field names
- **Vite Env Variables** — All environment variables used in Vite must start with `VITE_`
- **Final Report** — Always use the production URL (e.g., `project.vercel.app`), not `localhost`
