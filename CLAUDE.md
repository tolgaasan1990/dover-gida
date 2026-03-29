# CLAUDE.md — Frontend Website Rules

## Always Do First
- **Invoke the `frontend-design` skill** before writing any frontend code, every session, no exceptions.

## Reference Images
- If a reference image is provided: match layout, spacing, typography, and color exactly. Swap in placeholder content (images via `https://placehold.co/`, generic copy). Do not improve or add to the design.
- If no reference image: design from scratch with high craft (see guardrails below).
- Screenshot your output, compare against reference, fix mismatches, re-screenshot. Do at least 2 comparison rounds. Stop only when no visible differences remain or user says so.

## Local Server
- **Always serve on localhost** — never screenshot a `file:///` URL.
- Start the dev server: `node serve.mjs` (serves the project root at `http://localhost:3000`)
- `serve.mjs` lives in the project root. Start it in the background before taking any screenshots.
- If the server is already running, do not start a second instance.

## Screenshot Workflow
- Puppeteer is installed at `C:/Users/t.asan/AppData/Local/Temp/puppeteer-test/`. Chrome cache is at `C:/Users/t.asan/.cache/puppeteer/`.
- **Always screenshot from localhost:** `node screenshot.mjs http://localhost:3000`
- Screenshots are saved automatically to `./temporary screenshots/screenshot-N.png` (auto-incremented, never overwritten).
- Optional label suffix: `node screenshot.mjs http://localhost:3000 label` → saves as `screenshot-N-label.png`
- `screenshot.mjs` lives in the project root. Use it as-is.
- After screenshotting, read the PNG from `temporary screenshots/` with the Read tool — Claude can see and analyze the image directly.
- When comparing, be specific: "heading is 32px but reference shows ~24px", "card gap is 16px but should be 24px"
- Check: spacing/padding, font size/weight/line-height, colors (exact hex), alignment, border-radius, shadows, image sizing

## Output Defaults
- Single `index.html` file, all styles inline, unless user says otherwise
- Tailwind CSS via CDN: `<script src="https://cdn.tailwindcss.com"></script>`
- Placeholder images: `https://placehold.co/WIDTHxHEIGHT`
- Mobile-first responsive

## Brand Assets
- Always check the `brand_assets/` folder before designing. It may contain logos, color guides, style guides, or images.
- If assets exist there, use them. Do not use placeholders where real assets are available.
- If a logo is present, use it. If a color palette is defined, use those exact values — do not invent brand colors.

## Anti-Generic Guardrails
- **Colors:** Never use default Tailwind palette (indigo-500, blue-600, etc.). Pick a custom brand color and derive from it.
- **Shadows:** Never use flat `shadow-md`. Use layered, color-tinted shadows with low opacity.
- **Typography:** Never use the same font for headings and body. Pair a display/serif with a clean sans. Apply tight tracking (`-0.03em`) on large headings, generous line-height (`1.7`) on body.
- **Gradients:** Layer multiple radial gradients. Add grain/texture via SVG noise filter for depth.
- **Animations:** Only animate `transform` and `opacity`. Never `transition-all`. Use spring-style easing.
- **Interactive states:** Every clickable element needs hover, focus-visible, and active states. No exceptions.
- **Images:** Add a gradient overlay (`bg-gradient-to-t from-black/60`) and a color treatment layer with `mix-blend-multiply`.
- **Spacing:** Use intentional, consistent spacing tokens — not random Tailwind steps.
- **Depth:** Surfaces should have a layering system (base → elevated → floating), not all sit at the same z-plane.

## Hard Rules
- Do not add sections, features, or content not in the reference
- Do not "improve" a reference design — match it
- Do not stop after one screenshot pass
- Do not use `transition-all`
- Do not use default Tailwind blue/indigo as primary color

---

## Proje Bilgileri — Döver Gıda

### Şirket
- **İsim:** Döver Gıda
- **Sektör:** Toptan gıda tedarikçisi
- **Lokasyon:** Hürriyet, Namık Kemal Cd. N.54, 35400 Buca / İzmir
- **Telefon:** 0545 479 22 19
- **Hizmet bölgesi:** İzmir merkez ve yakın il-ilçeler
- **Öne çıkan ürünler:** Zeytin, Turşu, Piknik Grubu (reçel, peynir, hazır paketler)
- **Diğer ürünler:** Bakliyat, Baharat, Konserve, Bitkisel Yağlar, Kahvaltılık
- **Instagram:** @dovergida

### Hosting & Domain
- **Hosting:** Netlify (ücretsiz plan) — otomatik deploy, GitHub'a push = canlı güncelleme
- **GitHub repo:** https://github.com/tolgaasan1990/dover-gida
- **Branch:** main
- **Ana domain:** dovergida.com.tr (primary)
- **www:** www.dovergida.com.tr → otomatik yönlendirir
- **Türkçe domain:** dövergıda.com.tr (xn--dvergda-90a94c.com.tr) → domain alias
- **Netlify subdomain:** dovergida.netlify.app
- **SSL:** Let's Encrypt, otomatik yenileme
- **DNS sağlayıcı:** e-destek.com
- **DNS kayıtları:** A: 75.2.60.5, CNAME www: dovergida.netlify.app

### SEO & Google
- **Google Search Console:** Doğrulanmış (HTML dosyası yöntemi — google7fedac7f417527c2.html)
- **Sitemap:** /sitemap.xml (gönderildi, başarılı)
- **robots.txt:** mevcut
- **Meta tag'ler:** description, keywords, Open Graph, Twitter Card ekli
- **Canonical URL:** https://dovergida.com.tr/

### Teknik Yapı
- **Tek dosya:** index.html (tüm HTML, CSS, JS inline)
- **CSS:** Tailwind CSS CDN
- **Fontlar:** Playfair Display (display/serif) + DM Sans (body/sans)
- **Renk paleti:** forest (yeşil tonları), brand (amber/altın tonları), earth (toprak tonları), dark (koyu arka plan)
- **Logo:** brand_assets/logo.png (demirci figürü, kırmızı çekiçli)
- **Ürün görselleri:** brand_assets/piknik.png, brand_assets/bakliyat.png + Pexels stok görseller
- **Favicon:** brand_assets/logo.png

### Site Bölümleri (mevcut sıra)
1. Navbar (logo + menü + İletişim butonu)
2. Hero (merkezi, "Döver Gıda / Toptan Tedarik" + CTA butonları + bilgi şeridi)
3. Marquee (kayan ürün kategorileri — Zeytin, Turşu, Piknik Grubu öne çıkan)
4. Hakkımızda (dekoratif panel + açıklama + İzmir/Bölgesel Teslimat/Kalite ikonları)
5. Ürünler — Geniş Ürün Yelpazesi (8 kart: gradient arka plan + Pexels görseller)
6. Hizmetler — Uçtan Uca Tedarik Çözümleri (4 kart)
7. İletişim — Bize Ulaşın (3 tıklanabilir kart: adres→Google Maps, telefon→tel:, e-posta→mailto:)
8. Footer (logo, hızlı bağlantılar, çalışma saatleri, sosyal medya)

### Yapılması Gerekenler
- Google My Business'a web sitesi ekle (dovergida.com.tr)
- Diğer ürünler için gerçek fotoğraflar ekle (şu an Pexels stok kullanılıyor)
- Google indexleme bekleniyor (3-7 gün)
