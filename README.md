# DeltaKPI Clomosy Mobile

DeltaKPI mobil paneli için Clomosy kaynak dosyaları.

## Yerel Firebase ayarı

GitHub'a gerçek Firebase URL veya API key yazmayın. Geliştirme sırasında `clomosy/Main.tro` içindeki aşağıdaki placeholder değerleri yerel değerlerle doldurun:

```pascal
GAuthLoginUrl = 'FIREBASE_AUTH_LOGIN_URL';
GRtdbUrl = 'FIREBASE_RTDB_URL';
```

Commit öncesi kontrol:

```powershell
rg -n "AIza|identitytoolkit|firebaseio|firebaseapp|secret|token|password" .
```
