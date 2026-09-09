# DeltaKPI Mobil Uygulaması — Clomosy Derleme Hata Raporu

**Proje:** Atiker DeltaKPI Mobil Uygulaması  
**Geliştirme ortamı:** Clomosy (TRObject)  
**Unit adı:** Main  
**Dosya:** Main.tro  

---

## 1. Giriş

DeltaKPI mobil uygulaması Clomosy platformunda geliştirilirken Main unit derlemesi sırasında çeşitli hatalar alındı. Bu raporda yalnızca karşılaşılan hatalar listelenmiştir.

---

## 2. Derleme Hataları

### Hata 1 — Sözdizimi hatası (Satır 143)

**Hata mesajı:**

```
Unit "Main": Sözdizimi hatası. Eksik noktalı virgül, parantez veya begin/end bloğunu kontrol edin.
(Satır 143, Sütun 1)
Kaynak satır 143: {
Teknik ayrıntı: Unit Main: Syntax error.
Source position: 143,1
```

**Hatanın görüldüğü kod bölümü:**

```pascal
function MailOk(AMail: String): Integer;
var
  i: Integer;
{
```

**Açıklama:** Derleyici, `MailOk` fonksiyonunun gövde bloğu açılışında (`{`) sözdizimi hatası bildirdi. Hata, fonksiyon tanımından hemen sonraki yerel değişken bildirimi (`var`) ile ilişkili görünmektedir.

---

### Hata 2 — Sözdizimi hatası (Satır 392)

**Hata mesajı:**

```
Unit "Main": Sözdizimi hatası. Eksik noktalı virgül, parantez veya begin/end bloğunu kontrol edin.
(Satır 392, Sütun 28)
Kaynak satır 392: while ((p < Length(s)) and (adet < 6))
Teknik ayrıntı: Unit Main: Syntax error.
Source position: 392,28
```

**Hatanın görüldüğü kod bölümü:**

```pascal
while ((p < Length(s)) and (adet < 6))
```

**Açıklama:** `OneriListesi` fonksiyonu içindeki `while` döngüsünde sözdizimi hatası oluştu. Hata, `and` operatörünün bulunduğu sütunda (28) raporlandı.

---

### Hata 3 — Tanımsız değişken/prosedür hatası (Satır 1057)

**Hata mesajı:**

```
Unit Main: Unknown identifier or variable is not declared: 'AksiyonGit'.
Source position: 1057,13
```

**Hatanın görüldüğü kod bölümü:**

```pascal
void SheetAksiyon;
{
  SheetKapat;
  AksiyonGit;
}
```

**Açıklama:** `SheetAksiyon` prosedürü içinde `AksiyonGit` çağrıldığında derleyici bu tanımlayıcıyı tanımadığını bildirdi.

---

## 3. Geliştirme Sürecinde Karşılaşılan Diğer Hatalar

Main unit dışında veya farklı aşamalarda aşağıdaki hatalar da görüldü:

| Sıra | Hata türü | Açıklama |
|------|-----------|----------|
| 1 | Atama/karşılaştırma | `if (GIdToken = '')` ifadesinde tek eşittir (`=`) kullanımı |
| 2 | Desteklenmeyen özellik | `PasswordChar` özelliğinin Clomosy'de bulunmaması |
| 3 | Tip uyumsuzluğu | HTTP metodunun string (`'GET'`) olarak verilmesi |
| 4 | Bileşen özelliği | `TclMemo` üzerinde `clProSettings` kullanımı |
| 5 | Döngüsel referans | Ana Kod ile unit dosyaları arasında `uses Main` kullanımı |
| 6 | Unit bulunamadı | `uses uHttp` ifadesinde unit'in projede olmaması |
| 7 | Desteklenmeyen API | `ViewportPosition.Y` ifadesinin derlenmemesi |
| 8 | Sözdizimi | `try/except`, `Exit` ve prosedür içi `var` kullanımları |

---

## 4. Sonuç

Clomosy Main unit derlemesi sırasında toplam 3 ana derleme hatası kaydedildi:

1. Satır 143 — Sözdizimi hatası (`{`)
2. Satır 392 — Sözdizimi hatası (`while ... and ...`)
3. Satır 1057 — Tanımsız prosedür (`AksiyonGit`)

Bunlara ek olarak geliştirme sürecinde Clomosy platformuna özgü API ve sözdizimi uyumsuzluklarından kaynaklanan hatalar da gözlemlendi.
