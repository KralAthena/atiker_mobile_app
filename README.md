# DeltaKPI Mobile

DeltaKPI Mobile, Clomosy ile hazırlanmış mobil KPI takip panelidir. Uygulama; yöneticilerin, analistlerin ve firma kullanıcılarının KPI durumunu, uyarıları, aksiyon planlarını ve AI yönetici raporlarını mobil ekrandan hızlıca takip edebilmesi için geliştirilmiştir.

Bu repo Atiker için hazırlanan DeltaKPI web panelindeki temel akışların mobil karşılığını içerir.

## Özellikler

- Firebase Authentication ile e-posta/şifre girişi
- Firebase Realtime Database üzerinden canlı şirket verisi okuma
- Rol bazlı ekran görünürlüğü
- KPI kategori dağılımı grafiği
- Panel özeti grafiği
- Uyarı dağılımı grafiği
- Yönetici notu ve son AI rapor odağı
- Aksiyon planları özeti
- AI yönetici raporları özeti
- Mobil kullanım için sade üst menü, hızlı erişim menüsü ve alt navigasyon

## Rol Bazlı Görünürlük

Web paneldeki yetki mantığı mobil tarafa da yansıtılmıştır.

| Alan | Erişebilen roller |
| --- | --- |
| Genel bakış | company_admin, admin, manager, analyst, viewer |
| KPI yönetimi | company_admin, admin, manager, analyst |
| Analiz merkezi | company_admin, admin, manager, analyst |
| Uyarılar | company_admin, admin, manager, analyst, viewer |
| Aksiyon planları | company_admin, admin, manager |
| AI raporları | company_admin, admin, manager, analyst, viewer |

Uygulama içinde teknik rol adı üst bilgide gösterilmez; kullanıcıya şirket ve kullanıcı bilgisi daha sade şekilde sunulur.

## Proje Yapısı

```text
clomosy/
  Main.tro                    Ana çalışan Clomosy ekranı ve uygulama akışı
  uAuth.tro                   Yardımcı auth denemeleri
  uHttp.tro                   Yardımcı HTTP/Firebase denemeleri
  uDashboard*.tro             Dashboard yardımcı denemeleri
  uKpis.tro                   KPI ekran denemeleri
  uAnalysis.tro               Analiz ekran denemeleri
  uAlerts.tro                 Uyarı ekran denemeleri
  uTheme.tro                  Tema yardımcı denemeleri
```

Not: Şu an çalışan ana dosya `clomosy/Main.tro` dosyasıdır. Yardımcı `.tro` dosyaları önceki ayrıştırma ve modülerleştirme denemeleri için repoda tutulmuştur.

## Firebase Ayarı

Güvenlik nedeniyle gerçek Firebase API key ve Realtime Database URL değeri repoya eklenmemiştir.

Geliştirme sırasında `clomosy/Main.tro` içindeki placeholder değerleri kendi yerel Firebase değerlerinizle değiştirin:

```pascal
GAuthLoginUrl = 'FIREBASE_AUTH_LOGIN_URL';
GRtdbUrl = 'FIREBASE_RTDB_URL';
```

Örnek:

```pascal
GAuthLoginUrl = 'https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key=...';
GRtdbUrl = 'https://...firebasedatabase.app';
```

Bu değerleri commit etmeyin.

## Güvenlik Kontrolü

Commit veya push öncesi aşağıdaki kontrolü çalıştırın:

```powershell
rg -n "AIza|identitytoolkit|firebaseio|firebaseapp|PRIVATE KEY|client_secret|refresh_token|gho_|ghp_" .
```

Gerçek key veya token görünüyorsa push yapmadan önce dosyadan çıkarın.

## Çalıştırma

1. Projeyi Clomosy geliştirme ortamında açın.
2. `clomosy/Main.tro` dosyasındaki Firebase placeholder değerlerini yerel ortamınızda doldurun.
3. Uygulamayı Clomosy üzerinden çalıştırın.
4. Firebase üzerinde kayıtlı kullanıcı ile giriş yapın.

## Durum

Bu sürüm mobil dashboard, rol bazlı görünürlük, grafikler, uyarılar, aksiyon planları ve AI rapor özetlerini içeren çalışan ilk public sürümdür.
