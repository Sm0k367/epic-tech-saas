# Epic Tech AI Engineering - Unrestricted Media Generation SaaS

A powerful SaaS platform for generating any type of media with AI - text, images, music, videos, code, and more without restrictions. Built for the future of creation.

🌟 **Features**
*   **Unrestricted AI Chat Interface:** Generate any type of content through an intuitive chat experience.
*   **Multi-Modal Generation:** Support for text, images, audio, video, code, and continually expanding.
*   **Stripe Integration:** Seamless subscription management using your Stripe account.
*   **Real-time Interaction:** Live AI interaction (WebSocket support planned for future iterations).
*   **Usage Tracking:** Monitor your generations and understand your limits.
*   **Responsive Design:** Fully functional on desktop, tablet, and mobile devices.
*   **Dark Theme:** Modern and sleek cyberpunk-inspired aesthetic.

🛠 **Tech Stack**
*   **Frontend:** Next.js 14+, React 18+, TypeScript, Tailwind CSS v3+
*   **Backend:** Next.js API Routes, Prisma ORM
*   **Database:** PostgreSQL (recommended for Vercel deployment) or SQLite (for local development).
*   **Authentication:** NextAuth.js
*   **Payments:** Stripe (Subscriptions)
*   **AI Providers:**
    *   OpenAI (GPT models, DALL-E) - Primary
    *   (Extensible architecture for Anthropic, Replicate, Nvidia, Groq, and more as listed in your .env)
*   **Deployment:** Vercel (Recommended)

🚀 **Quick Start (Local Development)**

**1. Clone Your Repository & Install Dependencies**
   ```bash
   # First, create a new repository on GitHub (e.g., "epic-tech-ai-engineering")
   # Then, clone your empty repository:
   # git clone https://github.com/YOUR_USERNAME/epic-tech-ai-engineering.git
   # cd epic-tech-ai-engineering

   # (After the Agent provides you with the initial project files, copy them here)

   # Install dependencies:
   npm install
   ```

**2. Environment Setup**
   *   Copy the `.env.example` file to `.env.local`:
      ```bash
      cp .env.example .env.local
      ```
   *   Fill in your API keys and other environment variables in `.env.local`. **Never commit `.env.local` to GitHub.**
      *Key variables to set:*
      ```env
      # Database (adjust for your local setup or Vercel Postgres later)
      DATABASE_URL="postgresql://YOUR_DB_USER:YOUR_DB_PASSWORD@YOUR_DB_HOST:5432/epic_tech_ai_db"

      # NextAuth
      NEXTAUTH_URL="http://localhost:3000" # For local development
      NEXTAUTH_SECRET="generate-a-strong-secret-here" # Use a strong, random string

      # Stripe (Use your actual keys and Price ID)
      STRIPE_SECRET_KEY="sk_YOUR_STRIPE_SECRET_KEY"
      STRIPE_PUBLISHABLE_KEY="pk_YOUR_STRIPE_PUBLISHABLE_KEY"
      STRIPE_WEBHOOK_SECRET="whsec_YOUR_STRIPE_WEBHOOK_SECRET" # Get this after setting up webhook endpoint
      STRIPE_PRICE_ID="price_YOUR_EXISTING_STRIPE_PRICE_ID" # The one you provided: price_1RVIj6K5abcrIcyekWGIf3ch

      # OpenAI
      OPENAI_API_KEY="sk_YOUR_OPENAI_API_KEY" # The one you provided

      # Serper API Key
      SERPER_API_KEY="YOUR_SERPER_API_KEY"

      # Non-KYC API Keys (1 & 2)
      NONKYC_API_KEY_1="YOUR_NONKYC_API_KEY_1"
      NONKYC_API_SECRET_1="YOUR_NONKYC_API_SECRET_1"
      NONKYC_API_KEY_2="YOUR_NONKYC_API_KEY_2"
      NONKYC_API_SECRET_2="YOUR_NONKYC_API_SECRET_2"

      # Coinbase API Key
      COINBASE_API_KEY="YOUR_COINBASE_API_KEY"
      COINBASE_API_PRIVATE_KEY="YOUR_COINBASE_API_PRIVATE_KEY_PEM_FORMAT"
      COINBASE_USER_ID="YOUR_COINBASE_USER_ID"

      # Nvidia API Keys (1 & 2)
      NVIDIA_API_KEY_1="YOUR_NVIDIA_API_KEY_1"
      NVIDIA_API_KEY_2="YOUR_NVIDIA_API_KEY_2"

      # Vercel Integration API Keys (1, 2 & 3) - For potential programmatic Vercel interaction if needed
      VERCEL_API_KEY_1="YOUR_VERCEL_API_KEY_1"
      VERCEL_API_KEY_2="YOUR_VERCEL_API_KEY_2"
      VERCEL_API_KEY_3="YOUR_VERCEL_API_KEY_3"

      # Ngrok API Key
      NGROK_API_KEY="YOUR_NGROK_API_KEY"

      # AI-Tutor Keys
      AI_TUTOR_OPENAI_API_KEY="YOUR_AI_TUTOR_OPENAI_KEY"
      AI_TUTOR_GROQ_API_KEY="YOUR_AI_TUTOR_GROQ_KEY"
      ```

**3. Database Setup (using Prisma)**
   ```bash
   # Generate Prisma client (usually runs automatically after npm install via postinstall script)
   npx prisma generate

   # Apply database schema changes (creates tables based on schema.prisma)
   npx prisma db push 

   # Optional: Seed database with initial data (if a seed script is created)
   # npx prisma db seed
   ```

**4. Run Development Server**
   ```bash
   npm run dev
   ```
   Open [http://localhost:3000](http://localhost:3000) in your browser.

🔧 **Configuration Details**

*   **Stripe Integration:**
    *   Your primary subscription link: `https://buy.stripe.com/7sI3dlgcQ4uL0gMeUW` (This will be linked from the app).
    *   **Webhook Setup (Crucial for production):**
        1.  Go to your Stripe Dashboard → Developers → Webhooks.
        2.  Click "Add endpoint".
        3.  Endpoint URL: `https://YOUR_DEPLOYED_DOMAIN.com/api/webhooks/stripe` (e.g., your Vercel URL). For local testing, you might use Stripe CLI or ngrok.
        4.  Select events to listen to (as per your original README):
            *   `customer.subscription.created`
            *   `customer.subscription.updated`
            *   `customer.subscription.deleted`
            *   `invoice.payment_succeeded`
            *   `invoice.payment_failed`
        5.  Copy the "Signing secret" for this webhook and set it as `STRIPE_WEBHOOK_SECRET` in your `.env.local`.

*   **AI Providers:**
    *   The platform is designed to be extensible. Initially, OpenAI (GPT, DALL-E) will be the focus.
    *   Add API keys to `.env.local` to enable other providers as they are integrated.

📦 **Deployment (Vercel Recommended)**

1.  **Push to Your GitHub Repository:**
    ```bash
    git add .
    git commit -m "Initial commit of Epic Tech AI Engineering project"
    git branch -M main # Or your preferred default branch name
    # git remote add origin https://github.com/YOUR_USERNAME/epic-tech-ai-engineering.git
    git push -u origin main
    ```

2.  **Deploy to Vercel:**
    *   Sign up or log in to [Vercel](https://vercel.com).
    *   Click "Add New..." → "Project".
    *   Import your GitHub repository.
    *   Vercel should auto-detect it as a Next.js project.
    *   **Configure Environment Variables:** Go to Project Settings → Environment Variables on Vercel and add all the variables from your `.env.local` file. **This is critical for production.**
    *   Deploy.

3.  **Production Database Setup (Vercel Postgres Example):**
    *   In Vercel, go to the "Storage" tab of your project and create a new PostgreSQL database.
    *   Vercel will provide a `DATABASE_URL`. Update this environment variable in your Vercel project settings.
    *   After deployment, you might need to run Prisma migrations against the production database. This can often be done by adding a `postinstall` script in `package.json` that includes `prisma migrate deploy` or by running it manually via Vercel CLI or a one-off job if Vercel supports it for your plan. A common approach is `npx prisma migrate deploy` in the build command or a separate release phase script. For now, `npx prisma db push` is simpler for initial setup.

🎯 **Usage (Once Deployed & Subscribed)**
*   **Subscribe:** Users will click a "Get Started" or "Subscribe" button, which will redirect to your Stripe payment link.
*   **Access Dashboard:** After successful subscription (verified via webhook or by checking Stripe status), users gain access to the AI generation dashboard.
*   **Generate Content:** Use the intuitive interface to request various types of media.
*   **Download/Share:** Save or share generated content.

🔒 **Security Considerations**
*   **Authentication:** NextAuth.js for secure user sessions.
*   **API Protection:** API routes should be protected, ensuring only authenticated and subscribed users can access generation features.
*   **Rate Limiting:** Implement usage tracking and consider rate limiting to prevent abuse and manage costs.
*   **Webhook Verification:** Always verify Stripe webhook signatures.

📊 **Monitoring & Analytics (Future)**
*   Track user generations, popular features, and potential errors.
*   Integrate analytics for user engagement.

🛣 **Roadmap (High-Level Vision)**
*   **Advanced AI Models:** Integrate GPT-4 Vision, Claude 3, Gemini, etc.
*   **Music Generation:** Explore Suno AI, MusicLM, or similar integrations.
*   **Video Generation:** Look into RunwayML, Pika Labs, etc.
*   **Developer API:** Offer API access for external integrations (could be a higher tier).
*   **Team Features:** Collaboration, shared projects, and multi-user accounts.
*   **Custom Model Support:** Allow users to use fine-tuned models (advanced).
*   **Mobile App:** Potential React Native companion app.

💰 **Monetization**
*   **Primary Subscription Model:**
    *   **Pro Plan:** (e.g., $29/month, using your Stripe link: `https://buy.stripe.com/7sI3dlgcQ4uL0gMeUW`)
    *   Features: Unrestricted generation types (within fair use), priority processing, potential API access.

🤝 **Contributing**
(Standard open-source contribution guidelines if you plan to open-source parts of it or accept community contributions later)
1.  Fork the repository.
2.  Create your feature branch (`git checkout -b feature/AmazingFeature`).
3.  Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4.  Push to the branch (`git push origin feature/AmazingFeature`).
5.  Open a Pull Request.

📄 **License**
*   (Consider an appropriate license, e.g., MIT License if open-sourcing, or proprietary if not. For now, placeholder.)
*   This project will be proprietary unless otherwise specified. (Or choose MIT if you prefer)

🆘 **Support & Contact**
*   **Documentation:** (e.g., `docs.epictechai.com` - placeholder)
*   **Community Discord:** (Placeholder - consider creating one)
*   **Twitter/X:** [@EpicTechAI](https://x.com/EpicTechAI)
*   **Email:** [epictechai@gmail.com](mailto:epictechai@gmail.com)

🙏 **Acknowledgments**
*   OpenAI, Anthropic, Replicate, Stability AI, Google, Nvidia, Groq, and other AI pioneers.
*   Vercel for seamless hosting and deployment.
*   Stripe for robust payment processing.
*   The Next.js and React teams and the broader open-source community.

---
*Built with passion by the Epic Tech AI Engineering team.*
*Generate anything, create everything, no limits.*