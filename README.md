# BusinessTech-
Iam creating a well equipped business tool which will be Ai molded to serve business peope
    
{
  "name": "bstech",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  },
  "dependencies": {
    "next": "14.2.15",
    "react": "18.3.1",
    "react-dom": "18.3.1",
    "openai": "^4.57.0"
  },
  "devDependencies": {

{
  "compilerOptions": {
    "target": "es5",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": false,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,

    "plugins": [{ "name": "next" }],
    "paths": {
      "@/*": ["./*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
} 
    "@types/node": "^20.14.12",
    "@types/react": "^18.3.3",
    "@types/react-dom": "^18.3.0",
    "autoprefixer": "^10.4.19",
    "eslint": "^8.57.0",
    "eslint-config-next": "14.2.15",
    "postcss": "^8.4.39",
    "tailwindcss": "^3.4.10",
    "typescript": "^5.5.4"
  }
}
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
};

export default nextConfig; 
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}; 
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './app/**/*.{js,ts,jsx,tsx,mdx}',
    './components/**/*.{js,ts,jsx,tsx,mdx}',
    './lib/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  theme: {
    extend: {
      colors: {
        btech: {
          50: '#f5f7ff',
          100: '#ebf0ff',
          200: '#d9e4ff',
          300: '#bdd0ff',
          400: '#8ea7ff',
          500: '#6a7dff',
          600: '#4f64f0',
          700: '#3f4ec9',
          800: '#313f9d',
          900: '#2f3a7c',
        },
      },
      boxShadow: {
        glow: '0 18px 50px rgba(108, 128, 255, 0.24)',
      },
      backgroundImage: {
        radar: 'radial-gradient(circle at top, rgba(108,128,255,0.20), rgba(15,23,42,0) 42%)',
      },
    },
  },
  plugins: [],
};
/// <reference types="next" />
/// <reference types="next/image-types/global" />

// NOTE: This file should not be edited.

http://localhost:3000

/// <reference types="next" />
/// <reference types="next/image-types/global" />

// NOTE: This file should not be edited.
@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  color-scheme: dark;
}

html {
  scroll-behavior: smooth;
}

body {
  margin: 0;
  min-height: 100vh;
  font-family: Arial, Helvetica, sans-serif;
  background: #020817;
  color: #f8fafc;
}

* {
  box-sizing: border-box;
}

pre {
  white-space: pre-wrap;
  word-break: break-word;
}

input,
textarea,
select,
button {
  font: inherit;
}
export type CampaignForm = {
  businessName: string;
  description: string;
  audience: string;
  tone: string;
  platform: string;
  objective: string;
};

export type GeneratedCampaign = {
  summary: string;
  socialPost: string;
  adCopy: string;
  emailDraft: string;
};
import type { CampaignForm, GeneratedCampaign } from './types';

export function generateMarketingContent(form: CampaignForm): GeneratedCampaign {
  const businessName = form.businessName || 'Your business';
  const description =
    form.description || 'high-quality solutions that help customers grow faster';
  const audience = form.audience || 'modern buyers';
  const tone = form.tone || 'friendly and persuasive';
  const platform = form.platform || 'Instagram';
  const objective = form.objective || 'increase sales and customer trust';

  return {
    summary: `${businessName} helps ${audience} by delivering ${description}. The campaign is designed with a ${tone} voice and optimized for ${platform} to achieve ${objective}.`,
    socialPost: `🚀 ${businessName} is here to help you ${objective}.

${description.charAt(0).toUpperCase() + description.slice(1)} for ${audience} who want smarter, faster, better results.

✨ Why people choose us:
• Proven value
• Fast execution
• Clear, confident messaging

Ready to grow? DM us today or visit our website.

#${businessName.replace(/\s+/g, '').toLowerCase()} #${platform
      .toLowerCase()
      .replace(/\s+/g, '')} #businessgrowth #smallbusiness`,
    adCopy: `Headline: ${businessName} Helps ${audience} Grow Faster

Subheadline: Turn your next idea into measurable momentum.

Body: Get strategic support for ${description}. We help brands build trust, attract attention, and convert more customers with a clear and effective marketing plan.

CTA: Book a free strategy call today.`,
    emailDraft: `Subject: Grow your business with ${businessName}

Hi there,

If you are looking to ${objective}, ${businessName} is here to help.

We create ${description} that help ${audience} move from interest to action with clear messaging and practical strategy.

Whether you are launching a new offer or refreshing your brand presence, we can help you build momentum.

Let’s talk about your next growth opportunity.

Best,
The ${businessName} Team`,
  };
}
'use client';

import { useEffect, useState } from 'react';
import { generateMarketingContent } from '@/lib/generate-content';
import type { CampaignForm, GeneratedCampaign } from '@/lib/types';

const initialForm: CampaignForm = {
  businessName: '',
  description: '',
  audience: '',
  tone: 'friendly and persuasive',
  platform: 'Instagram',
  objective: 'increase leads and brand awareness',
};

const STORAGE_KEY = 'bstech_campaign_history';

export default function MarketingStudio() {
  const [form, setForm] = useState<CampaignForm>(initialForm);
  const [loading, setLoading] = useState(false);
  const [results, setResults] = useState<GeneratedCampaign | null>(null);
  const [history, setHistory] = useState<string[]>([]);

  useEffect(() => {
    const saved = window.localStorage.getItem(STORAGE_KEY);
    if (saved) {
      try {
        setHistory(JSON.parse(saved));
      } catch {
        setHistory([]);
      }
    }
  }, []);

  const updateField = (field: keyof CampaignForm, value: string) => {
    setForm((prev) => ({ ...prev, [field]: value }));
  };

  const handleSubmit = async (event: React.FormEvent<HTMLFormElement>) => {
    event.preventDefault();
    setLoading(true);

    try {
      const response = await fetch('/api/generate', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(form),
      });

      const data = await response.json();

      if (!response.ok) {
        throw new Error(data.error || 'Failed to generate campaign');
      }

      setResults(data);
    } catch (error) {
      const fallback = generateMarketingContent(form);
      setResults(fallback);
      console.error(error);
    } finally {
      setLoading(false);
      const nextEntry = form.businessName || 'Recent campaign';
      const nextHistory = [nextEntry, ...history].slice(0, 5);
      setHistory(nextHistory);
      window.localStorage.setItem(STORAGE_KEY, JSON.stringify(nextHistory));
    }
  };

  return (
    <div className="grid gap-8 lg:grid-cols-[0.9fr_1.1fr]">
      <form
        onSubmit={handleSubmit}
        className="rounded-[28px] border border-slate-800 bg-slate-900 p-6 shadow-glow"
      >
        <div className="mb-6">
          <p className="text-sm font-semibold uppercase tracking-[0.24em] text-btech-200">
            AI studio
          </p>
          <h2 className="mt-2 text-3xl font-black text-white">
            Create your campaign brief
          </h2>
        </div>

        <div className="space-y-5">
          <div>
            <label className="mb-2 block text-sm font-medium text-slate-200">
              Business name
            </label>
            <input
              value={form.businessName}
              onChange={(e) => updateField('businessName', e.target.value)}
              className="w-full rounded-2xl border border-slate-700 bg-slate-950 px-4 py-3 text-white outline-none transition focus:border-btech-500"
              placeholder="Example: Peak Studio"
            />
          </div>

          <div>
            <label className="mb-2 block text-sm font-medium text-slate-200">
              Business description
            </label>
            <textarea
              value={form.description}
              onChange={(e) => updateField('description', e.target.value)}
              rows={4}
              className="w-full rounded-2xl border border-slate-700 bg-slate-950 px-4 py-3 text-white outline-none transition focus:border-btech-500"
              placeholder="Describe the product or service you offer"
            />
          </div>

          <div>
            <label className="mb-2 block text-sm font-medium text-slate-200">
              Target audience
            </label>
            <input
              value={form.audience}
              onChange={(e) => updateField('audience', e.target.value)}
              className="w-full rounded-2xl border border-slate-700 bg-slate-950 px-4 py-3 text-white outline-none transition focus:border-btech-500"
              placeholder="Example: founders, local professionals"
            />
          </div>

          <div className="grid gap-5 sm:grid-cols-2">
            <div>
              <label className="mb-2 block text-sm font-medium text-slate-200">
                Tone
              </label>
              <select
                value={form.tone}
                onChange={(e) => updateField('tone', e.target.value)}
                className="w-full rounded-2xl border border-slate-700 bg-slate-950 px-4 py-3 text-white outline-none transition focus:border-btech-500"
              >
                <option>friendly and persuasive</option>
                <option>professional and premium</option>
                <option>bold and energetic</option>
                <option>trustworthy and practical</option>
              </select>
            </div>

            <div>
              <label className="mb-2 block text-sm font-medium text-slate-200">
                Platform
              </label>
              <select
                value={form.platform}
                onChange={(e) => updateField('platform', e.target.value)}
                className="w-full rounded-2xl border border-slate-700 bg-slate-950 px-4 py-3 text-white outline-none transition focus:border-btech-500"
              >
                <option>Instagram</option>
                <option>Facebook</option>
                <option>Google Ads</option>
                <option>Email</option>
                <option>LinkedIn</option>
              </select>
            </div>
          </div>

          <div>
            <label className="mb-2 block text-sm font-medium text-slate-200">
              Campaign objective
            </label>
            <input
              value={form.objective}
              onChange={(e) => updateField('objective', e.target.value)}
              className="w-full rounded-2xl border border-slate-700 bg-slate-950 px-4 py-3 text-white outline-none transition focus:border-btech-500"
              placeholder="Example: increase leads and brand visibility"
            />
          </div>

          <button
            type="submit"
            disabled={loading}
            className="mt-2 w-full rounded-2xl bg-btech-500 px-5 py-3 text-sm font-semibold text-white transition hover:bg-btech-400 disabled:cursor-not-allowed disabled:opacity-70"
          >
            {loading ? 'Generating...' : 'Generate campaign'}
          </button>
        </div>
      </form>

      <div className="space-y-6">
        <div className="rounded-[28px] border border-slate-800 bg-slate-900 p-6">
          <p className="text-sm font-semibold uppercase tracking-[0.24em] text-btech-200">
            Recent campaigns
          </p>
          {history.length === 0 ? (
            <p className="mt-4 text-slate-400">No campaigns saved yet.</p>
          ) : (
            <ul className="mt-4 space-y-3">
              {history.map((item, index) => (
                <li
                  key={`${item}-${index}`}
                  className="rounded-2xl border border-slate-800 bg-slate-950 px-4 py-3 text-slate-200"
                >
                  {item}
                </li>
              ))}
            </ul>
          )}
        </div>

        {results ? (
          <>
            <div className="rounded-[28px] border border-slate-800 bg-slate-900 p-6">
              <p className="text-sm font-semibold uppercase tracking-[0.24em] text-btech-200">
                Summary
              </p>
              <p className="mt-4 text-slate-200">{results.summary}</p>
            </div>

            <div className="rounded-[28px] border border-slate-800 bg-slate-900 p-6">
              <p className="text-sm font-semibold uppercase tracking-[0.24em] text-btech-200">
                Social post
              </p>
              <pre className="mt-4 text-slate-200">{results.socialPost}</pre>
            </div>

            <div className="rounded-[28px] border border-slate-800 bg-slate-900 p-6">
              <p className="text-sm font-semibold uppercase tracking-[0.24em] text-btech-200">
                Ad copy
              </p>
              <pre className="mt-4 text-slate-200">{results.adCopy}</pre>
            </div>

            <div className="rounded-[28px] border border-slate-800 bg-slate-900 p-6">
              <p className="text-sm font-semibold uppercase tracking-[0.24em] text-btech-200">
                Email draft
              </p>
              <pre className="mt-4 text-slate-200">{results.emailDraft}</pre>
            </div>
          </>
        ) : (
          <div className="rounded-[28px] border border-dashed border-slate-700 bg-slate-900/60 p-8 text-center text-slate-400">
            Your generated content will appear here.
          </div>
        )}
      </div>
    </div>
  );
}
import { NextResponse } from 'next/server';
import OpenAI from 'openai';
import { generateMarketingContent } from '@/lib/generate-content';
import type { CampaignForm } from '@/lib/types';

export async function POST(request: Request) {
  try {
    const body: CampaignForm = await request.json();

    if (!body.businessName || !body.description) {
      return NextResponse.json(
        { error: 'Business name and description are required.' },
        { status: 400 }
      );
    }

    const apiKey = process.env.OPENAI_API_KEY;

    if (apiKey) {
      const openai = new OpenAI({ apiKey });

      const prompt = `
        Create a short marketing campaign for this business.
        Business name: ${body.businessName}
        Description: ${body.description}
        Audience: ${body.audience || 'modern buyers'}
        Tone: ${body.tone || 'friendly and persuasive'}
        Platform: ${body.platform || 'Instagram'}
        Objective: ${body.objective || 'increase engagement'}

        Return valid JSON with keys: summary, socialPost, adCopy, emailDraft.
      `;

      const completion = await openai.chat.completions.create({
        model: 'gpt-4o-mini',
        temperature: 0.8,
        messages: [
          {
            role: 'system',
            content: 'You are a creative marketing strategist. Return valid JSON only.',
          },
          { role: 'user', content: prompt },
        ],
      });

      const content = completion.choices?.[0]?.message?.content || '{}';
      const parsed = JSON.parse(content);

      return NextResponse.json({
        summary:
          parsed.summary ||
          `Campaign for ${body.businessName} across ${body.platform || 'digital channels'}.`,
        socialPost: parsed.socialPost || generateMarketingContent(body).socialPost,
        adCopy: parsed.adCopy || generateMarketingContent(body).adCopy,
        emailDraft: parsed.emailDraft || generateMarketingContent(body).emailDraft,
      });
    }

    return NextResponse.json(generateMarketingContent(body));
  } catch (error) {
    console.error('Generate API error:', error);
    return NextResponse.json(
      { error: 'Something went wrong while generating content.' },
      { status: 500 }
    );
  }
}
import MarketingStudio from '@/components/MarketingStudio';

const featureCards = [
  {
    title: 'Campaign briefs',
    body: 'Turn raw business context into useful strategy, goals, and positioning.',
  },
  {
    title: 'AI content factory',
    body: 'Generate social posts, ads, email drafts, and launch copy in one workflow.',
  },
  {
    title: 'Campaign archive',
    body: 'Save your best ideas, iterate on them, and reuse winning campaigns quickly.',
  },
];

const plans = [
  {
    name: 'Starter',
    price: '$19',
    period: '/month',
    features: ['10 AI campaigns', 'Social content creator', 'History and saved drafts'],
  },
  {
    name: 'Growth',
    price: '$49',
    period: '/month',
    features: ['Unlimited campaigns', 'Ad + email generation', 'Multi-brand workspaces'],
    featured: true,
  },
  {
    name: 'Scale',
    price: 'Custom',
    period: 'Enterprise',
    features: ['Brand guidelines', 'API access', 'Priority support'],
  },
];

export default function HomePage() {
  return (
    <main className="min-h-screen bg-slate-950 text-white">
      <div className="bg-radar">
        <header className="mx-auto flex max-w-7xl items-center justify-between px-6 py-6 lg:px-10">
          <div className="flex items-center gap-3">
            <div className="flex h-10 w-10 items-center justify-center rounded-xl bg-gradient-to-br from-btech-500 to-btech-700 text-lg font-black text-white shadow-glow">
              B
            </div>
            <div>
              <p className="text-xl font-black tracking-tight">B/STech</p>
              <p className="text-xs uppercase tracking-[0.22em] text-slate-400">
                AI marketing engine
              </p>
            </div>
          </div>

          <nav className="hidden items-center gap-8 text-sm text-slate-300 md:flex">
            <a href="#features" className="transition hover:text-white">Features</a>
            <a href="#studio" className="transition hover:text-white">Studio</a>
            <a href="#pricing" className="transition hover:text-white">Pricing</a>
          </nav>

          <a
            href="#studio"
            className="rounded-full border border-slate-700 bg-slate-900 px-4 py-2 text-sm font-medium text-white transition hover:border-btech-500 hover:text-btech-200"
          >
            Launch campaign
          </a>
        </header>

        <section className="mx-auto grid max-w-7xl gap-10 px-6 pb-16 pt-10 lg:grid-cols-[1.2fr_0.8fr] lg:px-10 lg:pb-24 lg:pt-16">
          <div className="space-y-8">
            <div className="inline-flex items-center rounded-full border border-btech-500/30 bg-btech-500/10 px-4 py-2 text-xs font-semibold uppercase tracking-[0.22em] text-btech-200">
              built for modern brands
            </div>

            <div className="space-y-5">
              <h1 className="max-w-2xl text-4xl font-black tracking-tight text-white sm:text-5xl lg:text-6xl">
                Turn your business idea into a full marketing campaign.
              </h1>
              <p className="max-w-xl text-lg text-slate-300">
                B/STech helps startups, agencies, and founders create campaign strategy,
                ads, and content in minutes using AI-powered workflows.
              </p>
            </div>

            <div className="flex flex-wrap gap-4">
              <a
                href="#studio"
                className="rounded-full bg-btech-500 px-6 py-3 text-sm font-semibold text-white shadow-glow transition hover:bg-btech-400"
              >
                Generate content
              </a>
              <a
                href="#features"
                className="rounded-full border border-slate-700 bg-slate-900 px-6 py-3 text-sm font-semibold text-slate-200 transition hover:border-slate-500 hover:text-white"
              >
                Explore features
              </a>
            </div>

            <div className="grid gap-4 sm:grid-cols-3">
              <div className="rounded-2xl border border-slate-800 bg-slate-900/80 p-4">
                <p className="text-2xl font-black text-white">3x</p>
                <p className="text-sm text-slate-400">Faster campaign output</p>
              </div>
              <div className="rounded-2xl border border-slate-800 bg-slate-900/80 p-4">
                <p className="text-2xl font-black text-white">18+</p>
                <p className="text-sm text-slate-400">Marketing templates</p>
              </div>
              <div className="rounded-2xl border border-slate-800 bg-slate-900/80 p-4">
                <p className="text-2xl font-black text-white">24/7</p>
                <p className="text-sm text-slate-400">Creative coverage</p>
              </div>
            </div>
          </div>

          <div className="rounded-[28px] border border-slate-800 bg-slate-900/90 p-6 shadow-glow backdrop-blur-sm">
            <p className="text-xs font-semibold uppercase tracking-[0.24em] text-btech-200">
              Growth snapshot
            </p>
            <div className="mt-6 space-y-4">
              <div className="rounded-2xl border border-slate-800 bg-slate-950 p-4">
                <p className="text-sm text-slate-400">Use case</p>
                <p className="mt-1 font-semibold text-white">Local business growth</p>
              </div>
              <div className="rounded-2xl border border-slate-800 bg-slate-950 p-4">
                <p className="text-sm text-slate-400">Main goal</p>
                <p className="mt-1 font-semibold text-white">
                  Increase leads and conversions
                </p>
              </div>
              <div className="rounded-2xl border border-slate-800 bg-slate-950 p-4">
                <p className="text-sm text-slate-400">Best channels</p>
                <p className="mt-1 font-semibold text-white">
                  Instagram, search, email
                </p>
              </div>
            </div>
          </div>
        </section>
      </div>

      <section id="features" className="mx-auto max-w-7xl px-6 py-20 lg:px-10">
        <div className="mb-10 max-w-2xl">
          <p className="text-sm font-semibold uppercase tracking-[0.24em] text-btech-200">
            Features
          </p>
          <h2 className="mt-3 text-3xl font-black tracking-tight text-white sm:text-4xl">
            Built for ambitious businesses and lean teams
          </h2>
        </div>

        <div className="grid gap-6 md:grid-cols-3">
          {featureCards.map((item) => (
            <div
              key={item.title}
              className="rounded-3xl border border-slate-800 bg-slate-900 p-6"
            >
              <div className="mb-4 inline-flex rounded-2xl bg-btech-500/15 p-3 text-xl text-btech-200">
                ✦
              </div>
              <h3 className="text-xl font-bold text-white">{item.title}</h3>
              <p className="mt-3 text-slate-300">{item.body}</p>
            </div>
          ))}
        </div>
      </section>

      <section id="studio" className="mx-auto max-w-7xl px-6 pb-20 lg:px-10">
        <MarketingStudio />
      </section>

      <section id="pricing" className="mx-auto max-w-7xl px-6 pb-20 lg:px-10">
        <div className="mb-10 max-w-2xl">
          <p className="text-sm font-semibold uppercase tracking-[0.24em] text-btech-200">
            Plans
          </p>
          <h2 className="mt-3 text-3xl font-black tracking-tight text-white sm:text-4xl">
            Flexible pricing for growing brands
          </h2>
        </div>

        <div className="grid gap-6 md:grid-cols-3">
          {plans.map((plan) => (
            <div
              key={plan.name}
              className={
                plan.featured
                  ? 'rounded-3xl border border-btech-500 bg-btech-500/10 p-6 shadow-glow'
                  : 'rounded-3xl border border-slate-800 bg-slate-900 p-6'
              }
            >
              <p className="text-sm uppercase tracking-[0.26em] text-slate-400">
                {plan.name}
              </p>
              <p className="mt-4 text-4xl font-black text-white">{plan.price}</p>
              <p className="mt-2 text-slate-400">{plan.period}</p>
              <ul className="mt-6 space-y-3 text-slate-300">
                {plan.features.map((feature) => (
                  <li key={feature}>• {feature}</li>
                ))}
              </ul>
            </div>
          ))}
        </div>
      </section>

      <footer className="border-t border-slate-800 bg-slate-950/80">
        <div className="mx-auto flex max-w-7xl flex-col items-center justify-between gap-4 px-6 py-8 text-sm text-slate-400 md:flex-row lg:px-10">
          <p>© 2026 B/STech. Growth, simplified.</p>
          <div className="flex gap-5">
            <a href="#features" className="transition hover:text-white">Features</a>
            <a href="#studio" className="transition hover:text-white">Studio</a>
            <a href="#pricing" className="transition hover:text-white">Pricing</a>
          </div>
        </div>
      </footer>
    </main>
  );
}
# B/STech

B/STech is a SaaS-style AI marketing platform for startups, agencies, and growing businesses. It helps users create marketing briefs, ad copy, social posts, and email drafts from a simple campaign form.

## Features
- AI-powered marketing generator
- Landing page with pricing and CTA sections
- Marketing studio form
- Campaign history in browser storage
- Demo fallback when no OpenAI key is configured

## Stack
- Next.js
- TypeScript
- Tailwind CSS
- OpenAI API (optional)

## Local setup

1. Install dependencies:
```bash
npm install
import { createServerClient } from "@supabase/ssr";
import { cookies } from "next/headers";

export async function createSupabaseServerClient() {
  const cookieStore = await cookies();

  return createServerClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!,
    {
      cookies: {
        getAll() {
          return cookieStore.getAll();
        },
        setAll(cookiesToSet) {
          try {
            cookiesToSet.forEach(({ name, value, options }) => {
              cookieStore.set(name, value, options);
            });
          } catch {
            // Server components may not always be able to set cookies.
          }
        },
      },
    }
  );
}
import { NextResponse } from "next/server";
import { createSupabaseServerClient } from "@/lib/supabase/server";
import Stripe from "stripe";

const stripe = new Stripe(process.env.STRIPE_SECRET_KEY!, {
  apiVersion: "2024-06-20",
});

export async function POST() {
  const supabase = await createSupabaseServerClient();
  const {
    data: { user },
    error,
  } = await supabase.auth.getUser();

  if (error || !user) {
    return NextResponse.json({ error: "Sign in first." }, { status: 401 });
  }

  const appUrl = process.env.NEXT_PUBLIC_APP_URL || "http://localhost:3000";
  const priceId = process.env.STRIPE_PRICE_ID;

  if (!priceId) {
    return NextResponse.json(
      { error: "Stripe billing is not configured yet." },
      { status: 500 }
    );
  }

  const session = await stripe.checkout.sessions.create({
    mode: "subscription",
    line_items: [{ price: priceId, quantity: 1 }],
    customer_email: user.email || undefined,
    client_reference_id: user.id,
    success_url: `${appUrl}/dashboard?billing=success`,
    cancel_url: `${appUrl}/pricing?billing=cancelled`,
    metadata: {
      userId: user.id,
    },
  });

  return NextResponse.json({ url: session.url });
}
import { NextResponse } from "next/server";
import Stripe from "stripe";
import { createClient } from "@supabase/supabase-js";

const stripe = new Stripe(process.env.STRIPE_SECRET_KEY!, {
  apiVersion: "2024-06-20",
});

const supabaseAdmin = createClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,
  process.env.SUPABASE_SERVICE_ROLE_KEY!
);

export async function POST(request: Request) {
  const signature = request.headers.get("stripe-signature");

  if (!signature) {
    return NextResponse.json({ error: "Missing Stripe signature." }, { status: 400 });
  }

  try {
    const body = await request.text();
    const event = stripe.webhooks.constructEvent(
      body,
      signature,
      process.env.STRIPE_WEBHOOK_SECRET!
    );

    if (
      event.type === "checkout.session.completed" ||
      event.type === "customer.subscription.updated" ||
      event.type === "customer.subscription.deleted"
    ) {
      const object = event.data.object as Stripe.Checkout.Session | Stripe.Subscription;

      let subscription: Stripe.Subscription;
      let userId: string | null = null;
      let customerId: string | null = null;
      let email: string | null = null;

      if (object.object === "checkout.session") {
        const session = object as Stripe.Checkout.Session;
        userId = session.client_reference_id || null;
        customerId =
          typeof session.customer === "string"
            ? session.customer
            : session.customer?.id || null;
        email = session.customer_details?.email || null;

        if (session.subscription) {
          subscription = await stripe.subscriptions.retrieve(
            session.subscription as string
          );
        } else {
          return NextResponse.json({ received: true });
        }
      } else {
        subscription = object as Stripe.Subscription;
        userId = subscription.metadata.userId || null;
        customerId =
          typeof subscription.customer === "string"
            ? subscription.customer
            : subscription.customer?.id || null;
      }

      if (userId) {
        await supabaseAdmin.from("profiles").upsert(
          {
            id: userId,
            email: email || undefined,
            stripe_customer_id: customerId,
          },
          { onConflict: "id" }
        );

        await supabaseAdmin.from("subscriptions").upsert(
          {
            user_id: userId,
            stripe_subscription_id: subscription.id,
            status: subscription.status,
            price_id: subscription.items.data[0]?.price.id || null,
            current_period_end: subscription.current_period_end
              ? new Date(subscription.current_period_end * 1000).toISOString()
              : null,
            updated_at: new Date().toISOString(),
          },
          { onConflict: "user_id" }
        );
      }
    }

    return NextResponse.json({ received: true });
  } catch (error) {
    console.error("Webhook error:", error);
    return NextResponse.json(
      { error: "Invalid webhook signature." },
      { status: 400 }
    );
  }
}
create table public.profiles (
  id uuid primary key references auth.users(id) on delete cascade,
  email text,
  stripe_customer_id text,
  created_at timestamptz not null default now()
);

create table public.subscriptions (
  user_id uuid primary key references public.profiles(id) on delete cascade,
  stripe_subscription_id text unique,
  status text not null default 'inactive',
  price_id text,
  current_period_end timestamptz,
  updated_at timestamptz not null default now()
);

create table public.campaigns (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references public.profiles(id) on delete cascade,
  business_name text not null,
  brief jsonb not null,
  content jsonb not null,
  created_at timestamptz not null default now()
);

alter table public.profiles enable row level security;
alter table public.subscriptions enable row level security;
alter table public.campaigns enable row level security;

create policy "Users can view own profile" on public.profiles
for select using ((select auth.uid()) = id);

create policy "Users can update own profile" on public.profiles
for update using ((select auth.uid()) = id);

create policy "Users can view own subscription" on public.subscriptions
for select using ((select auth.uid()) = user_id);

create policy "Users can update own subscription" on public.subscriptions
for update using ((select auth.uid()) = user_id);

create policy "Users can manage own campaigns" on public.campaigns
for all using ((select auth.uid()) = user_id)
with check ((select auth.uid()) = user_id);
import { redirect } from "next/navigation";
import { createSupabaseServerClient } from "@/lib/supabase/server";

export default async function DashboardPage() {
  const supabase = await createSupabaseServerClient();
  const {
    data: { user },
    error,
  } = await supabase.auth.getUser();

  if (error || !user) {
    redirect("/login");
  }

  return (
    <main className="min-h-screen bg-slate-950 px-6 py-16 text-white lg:px-10">
      <div className="mx-auto max-w-6xl">
        <h1 className="text-4xl font-black tracking-tight">Dashboard</h1>
        <p className="mt-2 text-slate-400">Welcome back, {user.email}.</p>

        <div className="mt-8 grid gap-6 md:grid-cols-3">
          <div className="rounded-3xl border border-slate-800 bg-slate-900 p-6">
            <p className="text-sm text-slate-400">Campaigns</p>
            <p className="mt-3 text-3xl font-black text-white">42</p>
          </div>
          <div className="rounded-3xl border border-slate-800 bg-slate-900 p-6">
            <p className="text-sm text-slate-400">Leads generated</p>
            <p className="mt-3 text-3xl font-black text-white">1,284</p>
          </div>
          <div className="rounded-3xl border border-slate-800 bg-slate-900 p-6">
            <p className="text-sm text-slate-400">Avg. engagement</p>
            <p className="mt-3 text-3xl font-black text-white">7.9%</p>
          </div>
        </div>

        <div className="mt-8 rounded-3xl border border-slate-800 bg-slate-900 p-6">
          <h2 className="text-xl font-bold">Recent campaigns</h2>
          <div className="mt-4 space-y-4">
            {[
              "Spring launch recap",
              "Local service lead campaign",
              "Brand refresh creative sprint",
            ].map((item) => (
              <div
                key={item}
                className="rounded-2xl border border-slate-800 bg-slate-950 p-4 text-slate-200"
              >
                {item}
              </div>
            ))}
          </div>
        </div>
      </div>
    </main>
  );
}
export default function LoginPage() {
  return (
    <main className="flex min-h-screen items-center justify-center bg-slate-950 px-6 py-12 text-white">
      <div className="w-full max-w-md rounded-3xl border border-slate-800 bg-slate-900 p-8">
        <p className="text-sm font-semibold uppercase tracking-[0.24em] text-btech-200">
          Welcome back
        </p>
        <h1 className="mt-3 text-3xl font-black">Login to B/STech</h1>

        <div className="mt-8 space-y-4">
          <input
            className="w-full rounded-2xl border border-slate-700 bg-slate-950 px-4 py-3"
            placeholder="Email"
          />
          <input
            className="w-full rounded-2xl border border-slate-700 bg-slate-950 px-4 py-3"
            type="password"
            placeholder="Password"
          />
          <button className="w-full rounded-2xl bg-btech-500 px-5 py-3 font-semibold text-white">
            Sign in
          </button>
        </div>
      </div>
    </main>
  );
}
export default function SignUpPage() {
  return (
    <main className="flex min-h-screen items-center justify-center bg-slate-950 px-6 py-12 text-white">
      <div className="w-full max-w-md rounded-3xl border border-slate-800 bg-slate-900 p-8">
        <p className="text-sm font-semibold uppercase tracking-[0.24em] text-btech-200">
          Create account
        </p>
        <h1 className="mt-3 text-3xl font-black">
          Start building smarter campaigns
        </h1>

        <div className="mt-8 space-y-4">
          <input
            className="w-full rounded-2xl border border-slate-700 bg-slate-950 px-4 py-3"
            placeholder="Full name"
          />
          <input
            className="w-full rounded-2xl border border-slate-700 bg-slate-950 px-4 py-3"
            placeholder="Email"
          />
          <input
            className="w-full rounded-2xl border border-slate-700 bg-slate-950 px-4 py-3"
            type="password"
            placeholder="Password"
          />
          <button className="w-full rounded-2xl bg-btech-500 px-5 py-3 font-semibold text-white">
            Create account
          </button>
        </div>
      </div>
    </main>
  );
}
OPENAI_API_KEY=your_openai_api_key_here
NEXT_PUBLIC_APP_NAME=B/STech
NEXT_PUBLIC_APP_URL=http://localhost:3000

NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key

STRIPE_SECRET_KEY=sk_test_your_key
STRIPE_WEBHOOK_SECRET=whsec_your_key
STRIPE_PRICE_ID=price_your_price_id
import Stripe from "stripe";

export const stripe = new Stripe(process.env.STRIPE_SECRET_KEY!, {
  apiVersion: "2024-06-20",
});
import { createClient } from "@supabase/supabase-js";

export const supabaseBrowserClient = createClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,
  process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
);
# B/STech

B/STech is a SaaS-style AI marketing platform for startups, agencies, and growing businesses. It helps users create marketing briefs, ad copy, social posts, and email drafts from a simple campaign form.

## Features
- AI-powered marketing generator
- Landing page with pricing and CTA sections
- Marketing studio form
- Dashboard and pricing pages
- Stripe-ready and Supabase-ready foundation

## Stack
- Next.js
- TypeScript
- Tailwind CSS
- OpenAI API
- Stripe
- Supabase

## Local setup

1. Install dependencies:
```bash
npm install