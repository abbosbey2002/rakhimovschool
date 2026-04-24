---
name: uiux
description: Rahimov School loyihasi uchun UI/UX komponentlar, seksiyalar, animatsiyalar va parallax effektlar yaratadi. Foydalanuvchi yangi seksiya, karta, animatsiya, parallax, HTML/Tailwind komponent yoki dizayn so'raganda ishga tushsin.
---

Sen ushbu loyiha uchun maxsus UI/UX mutaxassisisan. Foydalanuvchi dizayn yoki komponent so'raganda quyidagi qoidalarga to'liq amal qilasan.

## TEXNOLOGIYALAR

- HTML5 — semantik teglar bilan
- Tailwind CSS — CDN orqali, mavjud `tailwind.config` kengaytirishdan foydalanish
- Vanilla JavaScript — jQuery yoki framework yo'q
- Tashqi kutubxona faqat zarurat bo'lganda (IntersectionObserver built-in, GSAP faqat murakkab animatsiyalar uchun)

## RANG PALITASI

```
brand-500: #07CA68   — asosiy yashil (tugmalar, ikonlar, aksent)
brand-600: #05b35b   — hover holati
brand-50:  #f0fdf4   — engil yashil fon
slate-900: #0f172a   — sarlavhalar
slate-600: #475569   — tavsif matni
slate-400: #94a3b8   — ikkinchi darajali matn
```

Shriftlar:
- Sarlavha: `font-heading` → Montserrat
- Matn: `font-body` → Inter (default body)

## SEKSIYA FONLARI TARTIBI

Seksiyalar almashinib boradi — bir xil fon yonma-yon kelmasin:

```
Juft:  bg-white
Toq:   bg-[#F8FAFC]
Dark:  bg-slate-900  — faqat CTA banner uchun
```

Padding: `py-20` (standart), `py-16` (kichik seksiyalar)
Container: `max-w-7xl mx-auto px-6 lg:px-8`

## SCROLL ANIMATSIYASI

Har qanday yangi element yoki seksiyaga shu pattern qo'shiladi.

CSS (bir marta `<style>` blokiga qo'sh, agar yo'q bo'lsa):
```css
.reveal {
  opacity: 0;
  transform: translateY(28px);
  transition: opacity 0.55s ease, transform 0.55s ease;
}
.reveal.visible {
  opacity: 1;
  transform: none;
}
```

JavaScript (bir marta `<script>` blokiga qo'sh, agar yo'q bo'lsa):
```js
const revealObserver = new IntersectionObserver((entries) => {
  entries.forEach(el => {
    if (el.isIntersecting) {
      el.target.classList.add('visible');
      revealObserver.unobserve(el.target);
    }
  });
}, { threshold: 0.15 });
document.querySelectorAll('.reveal').forEach(el => revealObserver.observe(el));
```

Ishlatish — har bir kartaga yoki seksiyaga `reveal` va `transition-delay` ber:
```html
<div class="reveal" style="transition-delay: 0ms">...</div>
<div class="reveal" style="transition-delay: 100ms">...</div>
<div class="reveal" style="transition-delay: 200ms">...</div>
```

## PARALLAX EFFEKTI

Fon dekoratsiya elementlariga ishlatiladi — kontent elementlarga EMAS.

JavaScript (bir marta `<script>` blokiga qo'sh):
```js
window.addEventListener('scroll', () => {
  const scrollY = window.scrollY;
  document.querySelectorAll('[data-parallax]').forEach(el => {
    const speed = parseFloat(el.dataset.parallax) || 0.3;
    el.style.transform = `translateY(${scrollY * speed}px)`;
  });
});
```

Ishlatish:
```html
<!-- Sekin harakat (fon doiralari, geometrik shakllar) -->
<div data-parallax="0.2" class="absolute -top-20 right-0 w-96 h-96
     bg-brand-500 rounded-full opacity-[0.04] blur-3xl pointer-events-none"></div>

<!-- Tezroq harakat -->
<div data-parallax="0.4" class="absolute bottom-0 left-0 ..."></div>
```

## KOMPONENT STANDARTLARI

### Karta
```html
<div class="bg-white border border-slate-200 rounded-2xl p-6
            hover:border-brand-200 hover:shadow-lg
            transition-all duration-250 group reveal">
  ...
</div>
```

### Primary tugma
```html
<a href="#" class="inline-flex items-center gap-2.5 px-7 py-3.5
                   bg-brand-500 hover:bg-brand-600 text-white
                   text-sm font-semibold rounded-xl
                   transition-colors shadow-md shadow-brand-500/25">
  Matn
  <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24">
    <path d="M9 18l6-6-6-6"/>
  </svg>
</a>
```

### Outline tugma
```html
<a href="#" class="inline-flex items-center gap-2.5 px-7 py-3.5
                   bg-white hover:bg-slate-50
                   border-2 border-brand-500 text-brand-600
                   text-sm font-semibold rounded-xl transition-colors">
  Matn
</a>
```

### Seksiya sarlavhasi
```html
<div class="text-center mb-14 reveal">
  <p class="text-sm font-semibold text-brand-600 uppercase tracking-widest mb-3">Kichik nom</p>
  <h2 class="text-3xl lg:text-4xl font-extrabold text-slate-900 tracking-tight">
    Asosiy sarlavha
  </h2>
  <p class="text-slate-500 mt-4 max-w-xl mx-auto">Qisqacha tavsif matni.</p>
</div>
```

### Badge
```html
<div class="inline-flex items-center gap-2 px-4 py-1.5
            bg-brand-50 border border-brand-100 rounded-full">
  <div class="w-2 h-2 bg-brand-500 rounded-full animate-pulse"></div>
  <span class="text-xs font-semibold text-brand-700 tracking-wide">Matn</span>
</div>
```

### Icon bloki
```html
<div class="w-12 h-12 bg-slate-100 rounded-xl flex items-center justify-center mb-5
            group-hover:bg-brand-500 transition-colors duration-200">
  <svg class="w-6 h-6 text-slate-600 group-hover:text-white transition-colors" ...></svg>
</div>
```

### Statistika karta
```html
<div class="stat-card bg-white border border-slate-200 rounded-2xl p-6 text-center
            hover:border-brand-200 reveal">
  <div class="w-12 h-12 bg-brand-50 rounded-xl flex items-center justify-center mx-auto mb-4">
    <svg class="w-6 h-6 text-brand-500" ...></svg>
  </div>
  <p class="text-3xl font-extrabold text-slate-900 font-heading">Raqam</p>
  <p class="text-sm font-semibold text-slate-700 mt-1">Nom</p>
  <p class="text-xs text-slate-400 mt-1.5">Tavsif</p>
</div>
```

## RESPONSIVLIK QOIDALARI

- Mobile-first: avval kichik ekran, keyin `lg:` bilan kengaytir
- Grid: `grid md:grid-cols-2 lg:grid-cols-3 gap-6`
- Yashirish: `hidden lg:flex` (desktop), `lg:hidden` (mobile)
- Matn o'lchami: `text-3xl lg:text-4xl` pattern

## QOIDALAR (har doim amal qil)

1. Har yangi element yoki seksiyaga `reveal` klass qo'sh
2. Staggered animatsiyada har 100ms kechikish ber
3. Parallax faqat fon dekoratsiya elementlariga — kontent matnga EMAS
4. Hover effektlari subtil: `hover:-translate-y-1.5`, katta sakrash yo'q
5. `transition-all duration-250` standart o'tish vaqti
6. Barcha ranglar brand palitasidan — tasodifiy hex kodi qo'shma
7. Har yangi seksiyaga `id` ber — navigatsiya ishlashi uchun
8. Yangi CSS yoki JS qo'shishdan avval `index.html` da mavjudligini tekshir
