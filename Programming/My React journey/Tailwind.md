🌀 1. Create a new React project with Vite
~~~bash
npm create vite@latest my-portfolio -- --template react-ts
cd my-portfolio
~~~
📦 2. Install Tailwind CSS and required packages
~~~bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
~~~
🧾 3. Configure `tailwind.config.js`
~~~bash
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}"
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
~~~
🎨 4. Create and edit `src/index.css`
~~~bash
@tailwind base;
@tailwind components;
@tailwind utilities;
~~~
### 🧠 5. Import `index.css` in `main.tsx`

Check that this line exists in `src/main.tsx`:
~~~bash
import './index.css';
~~~
🚀 6. Start the dev server
~~~bash
npm run dev
~~~
### ✅ 7. Test Tailwind is working

In `App.tsx`, replace content with:
~~~bash
function App() {
  return (
    <div className="text-3xl font-bold underline text-blue-500">
      Tailwind is working!
    </div>
  );
}

export default App;
~~~

<h1>If it is broken or not working </h>

✅ 1. Check Node Version

~~~bash
node -v
npm -v
~~~

### ✅ 2. Clean Everything

Run the following commands to fully reset `node_modules` and `package-lock.json`:
~~~bash
rm -rf node_modules package-lock.json
npm cache clean --force
npm install
~~~

Then reinstall Tailwind:
~~~bash
npm install -D tailwindcss postcss autoprefixer
~~~
### ✅ 3. Check if Tailwind CLI Exists

Run:
~~~bash
ls node_modules/.bin/
~~~
### ✅ 4. Use a Known Working Version

Force install a specific **older stable version** of Tailwind CSS CLI that is known to work well:
~~~
npm uninstall -D tailwindcss
npm install -D tailwindcss@3.4.1
npx tailwindcss init -p
~~~
### ✅ 5. (Optional) Use `pnpm` Instead

If you’re open to it, using `pnpm` often solves weird `npm` issues:
~~~bash
npm install -g pnpm
pnpm install
pnpm dlx tailwindcss init -p
~~~
