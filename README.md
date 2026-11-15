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

