
# ScheduleExcelExport – Kurulum Rehberi (Revit 2026)

Bu eklenti, Revit’te açık olan **Schedule (ViewSchedule)** görünümünü **biçimlendirilmiş gerçek Excel (.xlsx)** olarak dışa aktarır. Ribbon’da **Parlak Mühendislik** sekmesi altında bir buton olarak görünür.

## 1) Gereksinimler

* Autodesk **Revit 2026 (64-bit)**
* Windows
* Excel kurulu olmak zorunda değil (xlsx dosyası üretir; açmak için Excel/LibreOffice vb. gerekir)

> Not: Eklenti .NET Framework tabanlıdır; genelde Windows’ta gerekli bileşenler zaten vardır.

---

## 2) Kurulum klasörlerini oluştur

Aşağıdaki klasörü oluştur:

* `C:\RevitAddins\ScheduleExcelExport\`

---

## 3) Dosyaları doğru yerden kopyala

.RAR dosyasından çıkartılan dosyaların hepsini oluşturduğun `C:\RevitAddins\ScheduleExcelExport\` klasörünün içerisine yerleştir.


---

## 4) .addin dosyasını oluştur

Hedef bilgisayarda şu klasöre git:

* `%AppData%\Autodesk\Revit\Addins\2026\`

> Bu yolu açmak için: Windows’ta Çalıştır (Win+R) → yapıştır → Enter

Bu klasörde yeni bir dosya oluştur:

* `ScheduleExcelExport.addin`

Dosyanın içine şunu yapıştır:

```xml
<?xml version="1.0" encoding="utf-8" standalone="no"?>
<RevitAddIns>
  <AddIn Type="Application">
    <Name>Schedule Excel Export</Name>
    <Assembly>C:\RevitAddins\ScheduleExcelExport\ScheduleExcelExport.dll</Assembly>
    <AddInId>8D83C886-B739-4ACD-A9DB-1BC78F315B2A</AddInId>
    <FullClassName>ScheduleExcelExport.App</FullClassName>
    <VendorId>PRLK</VendorId>
    <VendorDescription>Parlak Mühendislik - Schedule XLSX Export</VendorDescription>
  </AddIn>
</RevitAddIns>
```

### Kritik notlar

* `<Assembly>` yolundaki DLL adı ve klasör yolu **birebir doğru** olmalı.
* `.addin` uzantısı yanlışlıkla `.addin.txt` olmasın.

  * Dosya Gezgini → Görünüm → “Dosya uzantıları”nı açıp kontrol et.

---

## 5) Revit’i başlat ve kontrol et

1. Revit 2026’yı kapat/aç (kurulumdan sonra ilk açılış gerekli)
2. Ribbon’da **Parlak Mühendislik** sekmesi gelmeli
3. Sekmede “Schedules” paneli içinde **Schedule Excel** butonu görünmeli

---

## 6) Kullanım

1. Revit’te bir Schedule aç (ör: Door Schedule)
2. **Parlak Mühendislik → Schedule Excel** butonuna tıkla
3. Dosya kaydetme penceresinde konum seç
4. `.xlsx` dosyası oluşturulur

---

## 7) Sorun giderme

### A) Ribbon sekmesi görünmüyor

* `.addin` dosyası doğru klasörde mi?

  * `%AppData%\Autodesk\Revit\Addins\2026\`
* `.addin` içindeki `<Assembly>` yolu doğru mu?
* Revit’i tamamen kapatıp yeniden açtın mı?

### B) “Could not load file or assembly ClosedXML…” hatası

Sebep: Bağımlı dll’ler aynı klasörde değil.

Çözüm:

* `bin\Release` içindeki **tüm** `.dll` dosyalarını
  `C:\RevitAddins\ScheduleExcelExport\` klasörüne tekrar kopyala.

### C) “RevitAPI.dll bulunamadı” gibi bir hata

Normalde olmaz (Revit kendi API dll’lerini sağlar). Eğer olursa:

* Yanlışlıkla Revit klasöründen dll kopyalayıp karıştırmış olabilirsin.
* Çözüm: Sadece eklenti klasörüne (C:\RevitAddins...) kendi çıktını koy.

### D) Buton var ama ikon yok

* Bu sadece görsel bir problem; eklenti yine çalışır.
* Çözüm (geliştirme tarafı): icon16.png / icon32.png dosyalarının “Embedded Resource” olduğundan emin olmak gerekir.

---

## 8) Kaldırma (Uninstall)

1. `%AppData%\Autodesk\Revit\Addins\2026\ScheduleExcelExport.addin` dosyasını sil
2. `C:\RevitAddins\ScheduleExcelExport\` klasörünü sil
3. Revit’i yeniden başlat

---
