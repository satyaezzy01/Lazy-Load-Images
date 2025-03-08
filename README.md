# Lazy Load Image Library

## 📌 Deskripsi
**Lazy Load Image Library** adalah skrip JavaScript ringan yang mengoptimalkan pemuatan gambar hanya saat masuk ke viewport. Ini membantu mempercepat waktu muat halaman dan meningkatkan performa web.

---

## 🔧 Instalasi
1. **Tambahkan file skrip** ke dalam HTML sebelum tag `</body>`:

   ```html
   <script src="lazyload.js" defer></script>
   ```

2. **Gunakan atribut `data-src` pada gambar** agar tidak dimuat sebelum masuk viewport:

   ```html
   <img class="lazyload" data-src="gambar.jpg" alt="Gambar Contoh" width="600" height="400">
   ```

---

## ⚡ Implementasi
Buat file `lazyload.js` dan tambahkan kode berikut:

```javascript
document.addEventListener("DOMContentLoaded", function () {
    let lazyImages = document.querySelectorAll("img.lazyload");

    if ("IntersectionObserver" in window) {
        let observer = new IntersectionObserver(function (entries, observer) {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    let img = entry.target;
                    img.src = img.dataset.src;
                    img.classList.remove("lazyload");
                    observer.unobserve(img);
                }
            });
        });

        lazyImages.forEach(img => observer.observe(img));
    } else {
        // Fallback untuk browser lama
        lazyImages.forEach(img => {
            img.src = img.dataset.src;
            img.classList.remove("lazyload");
        });
    }
});
```

---

## 🎨 CSS (Opsional)
Tambahkan efek blur sebelum gambar termuat sepenuhnya:

```css
.lazyload {
    filter: blur(10px);
    transition: filter 0.5s;
}

.lazyload.loaded {
    filter: blur(0);
}
```

---

## 📖 Cara Kerja
1. **Skrip mendeteksi semua gambar dengan class `lazyload`**.
2. **Saat gambar masuk viewport**, atribut `data-src` akan dipindahkan ke `src`.
3. **Jika browser mendukung `IntersectionObserver`**, skrip akan menghemat sumber daya dengan hanya memuat gambar yang diperlukan.
4. **Jika browser tidak mendukung `IntersectionObserver`**, semua gambar akan dimuat langsung.

---

## 📌 Keuntungan
✅ Mengurangi beban awal halaman web.<br>
✅ Meningkatkan kecepatan loading.<br>
✅ Kompatibel dengan browser modern dan menyediakan fallback untuk browser lama.<br>

---

## 🔗 Kontribusi
Jika ingin meningkatkan fitur atau melaporkan bug, silakan buat pull request atau issue di GitHub!

🔗 **Repository GitHub:** [Lazy Load Image Library](https://github.com/satyaezzy01)

---

## 📢 Lisensi
MIT License - Bebas digunakan dan dimodifikasi.
