服务端渲染（SSR）
    Google 搜索流量（SEO） 和 首屏加载速度（User Experience）。


{
  "dependencies": {
    "next": "latest",
    "react": "latest",
    "typescript": "latest",
    "tailwindcss": "latest",
    
    // 基础交互与 UI 层
    "lucide-react": "latest",     // 图标
    "zustand": "latest",         // 客户端状态管理
    "@tanstack/react-query": "", // 后端 API 请求与缓存
    "react-hook-form": "latest", // 高性能表单
    "zod": "latest",             // 数据类型与字段验证
    "framer-motion": "latest",   // 动效
    "sonner": "latest",          // 弹出提示
    
    // 核心商业与合规模块 🌟
    "next-intl": "latest",       // 国际化/多语言
    "@stripe/stripe-js": "latest",// Stripe 支付前端
    "stripe": "latest",          // Stripe 后端 SDK
    "next-auth": "beta",         // 安全身份认证 (Auth.js)
    "@prisma/client": "latest",  // 数据库安全连接 (ORM)
    
    // AI 与高级数据流 🌟
    "ai": "latest",              // Vercel AI SDK 文本/流式交互
    "recharts": "latest"         // 极致奢华的数据可视化图表
  }
}

my-ai-app/
├── public/                 # Static public assets (Favicons, global images)
└── src/
    ├── app/                # 🌐 THE ENGINE: Routing, Pages, and BFF API Gateways
    │   ├── [locale]/       # Next-intl wrapper for European Multi-language support (e.g., /en, /de)
    │   │   ├── (auth)/     # Auth Route Group (Hidden from URL path)
    │   │   │   ├── login/
    │   │   │   └── page.tsx
    │   │   ├── (dashboard)/# Main application workspace (Uses React Client-Side state)
    │   │   │   ├── analytics/
    │   │   │   └── page.tsx
    │   │   ├── api/        # 🛠️ NEXT.JS BFF (Backend-For-Frontend) GATEWAY
    │   │   │   ├── ai/
    │   │   │   │   └── route.ts  # Proxies frontend requests securely to Python FastAPI
    │   │   │   └── core/
    │   │   │   │   └── route.ts  # Proxies frontend requests securely to Java Spring Boot
    │   │   │   └── stripe/
    │   │   │       └── route.ts  # Handles incoming payment webhooks from Stripe
    │   │   ├── layout.tsx  # Global layout (Providers, Theme, Toaster injection)
    │   │   └── page.tsx    # C-End Marketing Homepage (Server-Side Rendered for SEO)
    │   
    ├── components/         # 🧱 GLOBAL UI BUILDING BLOCKS (Shared across all features)
    │   ├── ui/             # Atomic primitives (Buttons, Inputs, Dialogs via shadcn/ui)
    │   │   ├── button.tsx
    │   │   └── dialog.tsx
    │   ├── layouts/        # Shared structural layouts (Sidebar, Header, Footer)
    │   └── charts/         # Recharts wrapper configurations
    │
    ├── features/           # 🚀 DOMAIN MODULES (Encapsulated, self-contained business logic)
    │   ├── ai-prediction/  # Example Feature Bundle
    │   │   ├── components/ # Components exclusive to this feature (e.g., PredictionForm.tsx)
    │   │   ├── hooks/      # Feature-specific TanStack queries (`usePredictData.ts`)
    │   │   ├── services/   # Feature-specific internal API fetch handlers
    │   │   └── types.ts    # TypeScript definitions exclusive to this domain
    │   ├── billing/        # Subscription management feature bundle
    │   └── user-profile/   # Account management feature bundle
    │
    ├── hooks/              # 🎣 GLOBAL REACT HOOKS (Window size, theme, intersection observers)
    │   └── use-local-storage.ts
    │
    ├── lib/                # ⚙️ INSTANCE CONFIGURATIONS (Third-party client initializations)
    │   ├── prisma.ts       # Database client instance
    │   ├── stripe.ts       # Stripe gateway client config
    │   └── utils.ts        # Custom Tailwind utility class mergers (clsx/tailwind-merge)
    │
    ├── store/              # 🧠 GLOBAL CLIENT STATE (Zustand)
    │   ├── use-auth-store.ts
    │   └── use-ui-store.ts
    │
    ├── types/              # 🏷️ GLOBAL TYPESCRIPT SCHEMAS & INTERFACES
    │   ├── index.ts
    │   └── next-auth.d.ts  # NextAuth session overrides
    │
    └── messages/           # 🇩🇪 🇬🇧 🇫🇷 Localization Dictionaries for next-intl
        ├── en.json
        └── de.json






If you change [locale] to [anyw], the app will work exactly the same way technically, but the variable name you use in your code to read the URL will change from locale to anyw.
Next.js does not care what word you put inside the brackets; it simply treats whatever string is in there as a key name in a JavaScript object.
Here is the exact difference in how it alters your code under the hood:

1. How it works with [locale]

When a user visits ://mysite.com, Next.js creates a tracking parameters object that looks like this:
json
{ "locale": "de" }
Use code with caution.
Inside your page.tsx code, you would read the language selection like this:
typescript
export default async function Page({ params }: { params: { locale: string } }) {
  const currentLanguage = params.locale; // returns "de"
  // ...
}
Use code with caution.

2. How it works if you rename it to [anyw]

When a user visits ://mysite.com, Next.js now maps the exact same URL to your new key name:
json
{ "anyw": "de" }
Use code with caution.
To extract the language string inside your code, you are now forced to use your new variable name:
typescript
export default async function Page({ params }: { params: { anyw: string } }) {
  const currentLanguage = params.anyw; // still returns "de"
  // ...
}
Use code with caution.

⚠️ Why you shouldn't name it [anyw] in production

While Next.js doesn't care about the naming, third-party libraries do.
Because you are building an application for the European market and need multi-language support, you will be installing internationalization libraries like next-intl.
• These libraries are hardcoded to scan your folders looking specifically for the key name [locale].
• If you change the directory name to [anyw], next-intl will throw a runtime configuration error because it won't find the params.locale property it expects.

💡 Rule of Thumb

• Use [locale] for language sub-directories (industry standard).
• Use descriptive names like [id], [userId], or [productId] when building dynamic dynamic content pages (e.g., app/dashboard/users/[id]/page.tsx).
Are you ready to create your first page layout inside your project folder, or would you like to see how to build the Next.js API endpoint that will talk to your Python AI microservice next?
