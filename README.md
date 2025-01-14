# 프로젝트 생성

- `npm create vite@latest .`
  : `react` → `typescript`
- `npm i`
- `npm run dev` (확인용)

## 깃 셋팅

- `git init`
- `git remote add origin https://github.com/blendy9702/til-react-ts.git`

## ESLint 및 Prettire 셋팅

- `npm install --save-dev prettier eslint-config-prettier eslint-plugin-prettier`
- `npm i eslint-plugin-react`
- `.prettierrc` 파일 생성

```json
{
  "singleQuote": false,
  "semi": true,
  "useTabs": false,
  "tabWidth": 2,
  "trailingComma": "all",
  "printWidth": 80,
  "arrowParens": "avoid",
  "endOfLine": "auto"
}
```

- eslint.config.js

```js
import js from "@eslint/js";
import globals from "globals";
import reactHooks from "eslint-plugin-react-hooks";
import reactRefresh from "eslint-plugin-react-refresh";
import tseslint from "typescript-eslint";
import prettier from "eslint-plugin-prettier";
import react from "eslint-plugin-react";

export default tseslint.config(
  { ignores: ["dist"] },
  {
    extends: [js.configs.recommended, ...tseslint.configs.recommended],
    //검사할 파일 종류
    files: ["**/*.{ts,tsx,js,jsx}"],
    languageOptions: {
      ecmaVersion: 2020,
      globals: globals.browser,
    },
    plugins: {
      "react-hooks": reactHooks,
      "react-refresh": reactRefresh,
      prettier, // Prettier 플러그인
      react,
    },
    rules: {
      ...reactHooks.configs.recommended.rules,
      "react-refresh/only-export-components": [
        "warn",
        { allowConstantExport: true },
      ],
      "prettier/prettier": "warn", // Prettier 규칙 (포매팅 오류를 에러로 표시)
      "react/react-in-jsx-scope": "off", // React import 생략 가능
    },
    settings: {
      react: {
        version: "detect", // React 버전을 자동 감지
      },
    },
  },
);
```

## .gitignore

```
.env
.env.*
```

## 라이브러리

- npm i axios
- npm i react-router-dom
- npm i react-icons
- npm i react-hook-form
- npm i @hookform/resolvers
- npm i react-quill
- npm i swiper
- npm i antd --save
- npm i react-calendar

## Tailwindcss 셋팅

- npm install -D tailwindcss postcss autoprefixer
- npx tailwindcss init

- `npx tailwindcss init`
- tailwind.config.js

```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}", // Vite 프로젝트에 맞는 파일 확장자 추가
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

- vite.config.ts

```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "tailwindcss";

// https://vite.dev/config/
export default defineConfig({
  plugins: [react()],
  css: {
    postcss: {
      plugins: [tailwindcss()],
    },
  },
});
```

## Recoil 셋팅

- npm i recoil
- main.tsx

```tsx
import { RecoilRoot } from "recoil";
import { createRoot } from "react-dom/client";
import "./index.css";
import App from "./App.tsx";

createRoot(document.getElementById("root")!).render(
  <RecoilRoot>
    <App />
  </RecoilRoot>,
);
```

## tsconfig.app.json 을 통한 js 사용 설정

```json
// 추가 설정
"allowJs": true,
```

## proxy 사용 설정

- vite.config.js

```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "tailwindcss";

// https://vite.dev/config/
export default defineConfig({
  plugins: [react()],
  css: {
    postcss: {
      plugins: [tailwindcss()],
    },
  },
  server: {
    proxy: {
      "/api": {
        target: "http://192.168.0.144:5214",
        changeOrigin: true,
        secure: false,
      },
    },
  },
});
```
