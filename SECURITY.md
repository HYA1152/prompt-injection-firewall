# Security / Güvenlik

**English** | [Türkçe](#türkçe)

## Security check — 22 November 2026

After adding notebook `07_aile_deneyi.ipynb` and the files `results/aile_sonuclari.csv` and `results/aile_referans_yakalama.csv`: manual review by Hasan Yiğit Aydoğan, independently re-checked by Claude. Result: **no problems found.**

| Check | Result |
|---|---|
| API keys, tokens, passwords, private keys (files and full history) | None found |
| Private Google Drive file IDs | None (replaced by a placeholder in notebooks) |
| E-mail addresses | None found |
| Notebook outputs | Cleared (0 outputs) |
| New CSV files | Aggregate numbers only, no dataset texts |
| `.gitignore` still blocks `.env`, keys, datasets and per-example files | Tested, all ignored |

## Security check — 13 November 2026

Manual review by Hasan Yiğit Aydoğan, independently re-checked by Claude (automated scan of all tracked files and the full commit history). Result: **no problems found.**

| Check | Result |
|---|---|
| API keys, tokens, passwords, private keys in files | None found |
| The same patterns in the full commit history | None found |
| E-mail addresses or personal paths in files | None found |
| Notebook outputs (could leak data or paths) | All cleared (0 outputs) |
| Notebook metadata (Colab) | Only `provenance: []`, no account info |
| `.gitignore` blocks `.env`, `*.pem`, `*.key`, credentials, `*.csv`, model files | Tested, all ignored |
| Datasets or trained models committed | None (reproduced by the notebooks) |

### Rules for this repository

- Never commit `.env` files, API keys, Hugging Face / GitHub tokens or Google credentials.
- Never commit datasets, results CSVs or trained model files; notebooks regenerate them.
- Clear notebook outputs before committing.
- Before every commit, scan new files (including contributions from the co-author).
- If a secret is ever committed: revoke it immediately, then clean the history. Deleting the file in a new commit is not enough.

### Reporting

Open an issue or contact the repository owner if you find a security problem.

---

<a id="türkçe"></a>

# Türkçe

## Güvenlik kontrolü — 22 Kasım 2026

`07_aile_deneyi.ipynb` defteri ile `results/aile_sonuclari.csv` ve `results/aile_referans_yakalama.csv` dosyaları eklendikten sonra Hasan Yiğit Aydoğan elle kontrol etti, Claude bağımsız olarak tekrar kontrol etti. Sonuç: **sorun bulunmadı.**

| Kontrol | Sonuç |
|---|---|
| API anahtarı, token, parola, özel anahtar (dosyalar ve tüm geçmiş) | Yok |
| Özel Google Drive dosya numaraları | Yok (defterlerde yer tutucuyla değiştirildi) |
| E-posta adresi | Yok |
| Defter çıktıları | Temiz (0 çıktı) |
| Yeni CSV dosyaları | Yalnızca toplu sayılar, veri seti metni yok |
| `.gitignore`: `.env`, anahtarlar, veri setleri ve örnek başına dosyalar | Denendi, hepsi engelleniyor |

## Güvenlik kontrolü — 13 Kasım 2026

Hasan Yiğit Aydoğan elle kontrol etti, Claude bağımsız olarak tekrar kontrol etti (izlenen tüm dosyalar ve tüm commit geçmişi otomatik tarandı). Sonuç: **sorun bulunmadı.**

| Kontrol | Sonuç |
|---|---|
| Dosyalarda API anahtarı, token, parola, özel anahtar | Yok |
| Aynı desenler tüm commit geçmişinde | Yok |
| Dosyalarda e-posta adresi veya kişisel yol | Yok |
| Defter çıktıları (veri/yol sızdırabilir) | Hepsi temiz (0 çıktı) |
| Defter üst verisi (Colab) | Sadece `provenance: []`, hesap bilgisi yok |
| `.gitignore`: `.env`, `*.pem`, `*.key`, kimlik bilgileri, `*.csv`, model dosyaları | Denendi, hepsi engelleniyor |
| Depoya konmuş veri seti veya eğitilmiş model | Yok (defterler yeniden üretir) |

### Bu depo için kurallar

- `.env` dosyalarını, API anahtarlarını, Hugging Face / GitHub token'larını ve Google kimlik bilgilerini asla commit etmeyin.
- Veri setlerini, sonuç CSV'lerini ve eğitilmiş modelleri commit etmeyin; defterler bunları yeniden üretir.
- Commit'ten önce defter çıktılarını temizleyin.
- Her commit'ten önce yeni dosyaları (ortak yazarın eklediği dosyalar dahil) tarayın.
- Bir sır yanlışlıkla commit edilirse önce anahtarı hemen iptal edin, sonra geçmişi temizleyin. Dosyayı yeni bir commit'te silmek yetmez.

### Bildirim

Güvenlik sorunu bulursanız issue açın veya depo sahibiyle iletişime geçin.
