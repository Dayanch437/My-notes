### 🤖 What is `robots.txt`?

`robots.txt` is a simple text file placed in the **root directory** of your website (like `https://example.com/robots.txt`). It tells **search engine bots** (like Googlebot) which pages or folders they are allowed or not allowed to crawl.

It's not for security — just a guide for crawlers.

### 🛠️ How to Write `robots.txt`

#### ✅ Allow all bots to crawl everything:

~~~makefile
User-agent: *
Disallow:
~~~

❌ Block all bots from the entire site:
~~~makefile
User-agent: *
Disallow: /
~~~
❌ Block bots from a specific folder (e.g., `/admin/`):
~~~makefile
User-agent: *
Disallow: /admin/
~~~
✅ Allow Googlebot but block others:
~~~makefile
User-agent: Googlebot
Disallow:

User-agent: *
Disallow: /
~~~
✅ Add sitemap link (recommended):
~~~makefile
Sitemap: https://example.com/sitemap.xml
~~~
📌 Example for a typical website:
~~~makefile
User-agent: *
Disallow: /admin/
Disallow: /login/
Allow: /

Sitemap: https://dayanch.me/sitemap.xml
~~~

### 🔄 Where to place it?

Upload it to the **root** of your website:

~~~arduino
https://dayanch.me/robots.txt
~~~
