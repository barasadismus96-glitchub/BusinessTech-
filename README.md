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