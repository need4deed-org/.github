# 🌍 Need4Deed: Empowering Refugee Support in Berlin

### *Connecting volunteers with the real-time needs of accommodation centers.*

## 📖 About Need4Deed

**Need4Deed** is a Berlin-based NGO (funded by the EU and the Berlin Senate) dedicated to making volunteering for refugees more effective, transparent, and sustainable.

Our platform acts as a digital bridge:

* **For Volunteers:** Find specific tasks (translation, childcare, sports, tutoring) based on your language skills and location.
* **For Accommodation Centers:** Easily request specific help and manage volunteer support without administrative overhead.
* **For Society:** Fostering integration through direct, migrant-to-migrant and community support.

---

## 🏗 Project Architecture

The Need4Deed platform is split into three main parts to ensure scalability and developer focus:

| Repository | Tech Stack | Description |
| --- | --- | --- |
| **[Frontend (FE)](https://github.com/need4deed-org/fe)** | Next.js, TypeScript, PWA | The volunteer dashboard and public-facing landing page. |
| **[Backend (BE)](https://github.com/need4deed-org/be)** | Node.js, TypeORM, PostgreSQL | The core API managing users, deeds (tasks), and matches. |
| **[SDK](https://github.com/need4deed-org/sdk)** | TypeScript | Shared types and helpers to keep FE and BE in sync. |

---

## 🚀 Getting Started (Local Development)

We recommend a **sibling-folder setup** so the Frontend can correctly link to the local SDK.

### 1. Clone the Ecosystem

```bash
git clone https://github.com/need4deed-org/fe.git
git clone https://github.com/need4deed-org/be.git
git clone https://github.com/need4deed-org/sdk.git

```

### 2. Setup the Backend

```bash
cd be
npm install
# Copy .env.example to .env and configure your DB
npm start

```

### 3. Setup the Frontend

```bash
cd ../fe
npm install
# Link the local SDK for type safety
npm install ../sdk
npm run dev

```

Visit `http://localhost:3000` to see the app in action.

---

## 🤝 Contributing

We love our contributors! Whether you are a senior dev or looking for your first open-source contribution, your code helps real people in Berlin.

### Quick Start:

1. **Find an Issue:** Look for the `good first issue` or `help wanted` labels.
2. **Follow Design:** We use **Figma** for all UI. Please check the linked design in the issues before styling.
3. **Branching:** Use `yourname/feature-name`.
4. **Commits:** We use emojis to keep history readable!
* 🎨 — Styling/UI
* 🐛 — Bug fixes
* ✨ — New features
* 📝 — Documentation



---

## 🗺 Roadmap & Goals

* [ ] **Full PWA Support:** Enabling volunteers to get notifications on their phones.
* [ ] **Automated Matching:** Smart-matching volunteers' languages with center needs.
* [ ] **NGO Dashboard:** Advanced analytics for accommodation center managers.

---

## 📞 Contact & Community

* **Website:** [need4deed.org](https://www.need4deed.org)
* **Email:** [info@need4deed.org](mailto:info@need4deed.org)
* **Location:** Berlin, Germany

---

*Built with ❤️ by Nadav, Arturas and the Need4Deed Open Source Community.*
