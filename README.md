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