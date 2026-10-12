# Notoloji

okuma, yazma ve not alma üzerine — [notoloji.com](https://notoloji.com)

Jekyll ile yapılmış, GitHub Pages'te yayınlanan statik bir blog. `main` dalına her gönderimde GitHub Actions siteyi derleyip yayınlar.

## Yazmak

İki tür girdi var:

| Tür | Klasör | Başlık | Akışta |
|---|---|---|---|
| Not | `_posts/notlar/` | yok | tam metin |
| Yazı | `_posts/yazilar/` | var | başlık + özet |

### Not

`_posts/notlar/2026-10-12-1430.md` (dosya adı: tarih + saat)

Notun adresi, micro.blog'daki gibi metnin ilk beş kelimesinden üretilir: `/2026/10/12/kalemle-okumak-bir-konusmaya-donusur/`. Yayımladıktan sonra notun ilk kelimelerini değiştirirsen adres de değişir. Eski adresi korumak için ön bilgiye `slug: eski-adres` ekle.

```markdown
---
date: 2026-10-12 14:30:00 +0300
tags: [kalem, defter]
---
Notun metni.
```

### Yazı

`_posts/yazilar/2026-10-12-yazinin-adi.md`

```markdown
---
title: "Yazının başlığı"
date: 2026-10-12 14:30:00 +0300
tags: [okuma]
ozet: "Akışta görünecek kısa özet. Boş bırakılırsa ilk paragraf kullanılır."
---
Yazının metni.
```

### Obsidian'dan yayın

Kasadaki `Notoloji/` klasörüne yaz, özelliklere `tür: not` ya da `tür: yazı` ekle (şablonlar: `T_Notoloji Not`, `T_Notoloji Yazı`). Obsidian'daki **Notoloji'de yayınla** komutu (Shell commands eklentisi) şunu çalıştırır:

```bash
python3 scripts/yayinla.py
```

Betik klasörü siteyle eşitler: yeni ve değişen notları `_posts/` altına yazar, kasadan silineni ya da `tür`ü kaldırılanı siteden de kaldırır, `[[bağlantıları]]` ve `![[görselleri]]` dönüştürür, sonra commit edip yükler. İlk yayında nota `yayın` ve `adres` özelliklerini ekler; adres ve tarih bundan sonra sabit kalır. `--kuru` ne olacağını gösterir, hiçbir şey yazmaz.

### Kısayollar

```bash
./scripts/yeni-not.sh kalem,defter
./scripts/yeni-yazi.sh "Yazının başlığı" okuma
```

Telefondan yazmak için: GitHub uygulaması ya da github.com üzerinden ilgili klasörde **Add file → Create new file**.

## Sayfalar

- `/` — karışık akış (15 girdi/sayfa)
- `/yazilar/`, `/notlar/`, `/etiketler/`, `/arsiv/`, `/hakkinda/`
- `/feed.xml` (RSS) ve `/feed.json` (JSON Feed). Notlar başlıksız gider, micro.blog bunları kısa not olarak tanır.

## İsteğe bağlı

`_config.yml` içinde:

- `mastodon:` — Mastodon profilinde siteyi doğrulamak için `rel="me"` bağlantısı
- `webmention:` — webmention.io ile gelen yanıtları almak için
