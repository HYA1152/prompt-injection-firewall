# prompt-injection-firewall

**English** | [Türkçe](#türkçe)

Detecting prompt-injection attacks against Large Language Models (LLMs) with a Transformer-based "AI firewall" (fine-tuned BERT and RoBERTa), and measuring how well it **generalizes to datasets it has never seen**.

Congress paper: *Detection of Prompt Injection Attacks Against Large Language Models with a Transformer-Based AI Firewall and Evaluation of Generalization Performance* — 6th International Multidisciplinary Student Congress in the Light of Science, 17–19 November 2026 (online).

Authors: Hasan Yiğit Aydoğan, Ahmet İlter İnci. Advisor: Asst. Prof. Kubilay Ayturan. Gazi University, TUSAŞ Kazan Vocational School.

## Idea

A firewall for text: before a prompt reaches a chat model, a classifier labels it **0 = benign** or **1 = malicious (prompt injection / jailbreak)**. The question is not "how high is the accuracy on the same data?" but "what happens on an attack style the model has never seen?"

## Method (short)

1. **Data**: three public Hugging Face datasets as main data (`neuralchemy/Prompt-injection-dataset`, `xTRam1/safe-guard-prompt-injection`, `wambosec/prompt-injections`) and two as external tests (`jackhhao/jailbreak-classification`, `deepset/prompt-injections`).
2. **Cleaning / leakage control**: trimming, de-duplication, removal of texts with conflicting labels, removal of texts shared between datasets, group-aware split for `neuralchemy` (`group_id`).
3. **Models**: `bert-base-uncased` and `roberta-base`, fine-tuned for binary classification (downloaded automatically from Hugging Face with `from_pretrained`).
4. **Evaluation**: leave-one-dataset-out (train on two main datasets, test on the third), a same-distribution reference run, and the two external test sets. Metrics: accuracy, precision, recall, F1, ROC-AUC and true-positive rate at a low false-positive rate.
5. **Baseline**: a simple keyword/regex filter.

```
datasets ──► clean + de-duplicate ──► fine-tune BERT / RoBERTa ──► evaluate on unseen datasets
                                                                        │
                                              keyword-filter baseline ──┘ (comparison)
```

## Repository layout

| File | Purpose |
|---|---|
| `01_veri_inceleme.ipynb` | Look at the candidate datasets (columns, labels, examples) |
| `02_isinma_egitimi.ipynb` | Warm-up fine-tuning to check the pipeline works (not reported in the paper) |
| `03_veri_hazirlama.ipynb` | Merge, clean, de-duplicate, leakage control, produce `veri_birlesik.csv` |
| `04_anahtar_kelime_filtresi.ipynb` | Keyword/regex baseline |
| `05_…`, `06_…` | Main training/evaluation and multi-seed runs (added when the final runs finish) |

The notebooks are written for Google Colab (a free GPU is enough) and their explanations are in Turkish.

## Reproducing

- The datasets are **not stored in this repository**. Notebook `03` downloads the public datasets from Hugging Face and writes `veri_birlesik.csv` itself.
- Run the notebooks in order (`01` → `06`) in Colab.
- No API keys or credentials are needed or stored here. Never commit `.env` files or tokens (they are in `.gitignore`).

## Status

Work in progress. Final results and figures will be added here after the last runs are complete; no numbers are claimed before that.

## License / data

Check the license of each dataset on its Hugging Face page before reuse.

---

<a id="türkçe"></a>

# Türkçe

[English](#prompt-injection-firewall) | **Türkçe**

Büyük dil modellerine (LLM) yönelik prompt injection saldırılarını, Transformer tabanlı bir "yapay zekâ güvenlik duvarı" (ince ayar yapılmış BERT ve RoBERTa) ile tespit etme ve bu sistemin **hiç görmediği veri setlerinde** ne kadar başarılı olduğunu ölçme çalışması.

Kongre bildirisi: *Büyük Dil Modellerine Yönelik Prompt Injection Saldırılarının Transformer Tabanlı Bir Yapay Zekâ Güvenlik Duvarı ile Tespiti ve Genelleme Başarısının Değerlendirilmesi* — 6. Uluslararası Multidisipliner Öğrenci Kongresi (6th International Multidisciplinary Student Congress in the Light of Science), 17–19 Kasım 2026 (online).

Yazarlar: Hasan Yiğit Aydoğan, Ahmet İlter İnci. Danışman: Dr. Öğr. Üyesi Kubilay Ayturan. Gazi Üniversitesi, TUSAŞ Kazan Meslek Yüksekokulu.

## Fikir

Metin için bir güvenlik duvarı: bir istem (prompt) sohbet modeline ulaşmadan önce bir sınıflandırıcı onu **0 = zararsız** veya **1 = zararlı (prompt injection / jailbreak)** olarak etiketler. Asıl soru "aynı veride doğruluk kaç?" değil, "model daha önce hiç görmediği bir saldırı tarzında ne yapıyor?"

## Yöntem (kısaca)

1. **Veri**: Ana veri olarak üç açık Hugging Face veri seti (`neuralchemy/Prompt-injection-dataset`, `xTRam1/safe-guard-prompt-injection`, `wambosec/prompt-injections`), dış test olarak iki veri seti (`jackhhao/jailbreak-classification`, `deepset/prompt-injections`).
2. **Temizlik / sızıntı kontrolü**: boşluk kırpma, tekilleştirme, çelişkili etiketlerin atılması, veri setleri arasında ortak metinlerin atılması, `neuralchemy` için grup bazlı bölme (`group_id`).
3. **Modeller**: `bert-base-uncased` ve `roberta-base`, ikili sınıflandırma için ince ayar (Hugging Face'ten `from_pretrained` ile otomatik indirilir).
4. **Ölçüm**: bir veri setini dışarıda bırakma (iki ana veri setiyle eğit, üçüncüsünde test et), aynı dağılımda referans koşu ve iki dış test seti. Metrikler: doğruluk, kesinlik, duyarlılık, F1, ROC-AUC ve düşük yanlış pozitif oranında doğru pozitif oranı.
5. **Kıyas**: basit anahtar kelime / regex filtresi.

## Depo yapısı

| Dosya | Amaç |
|---|---|
| `01_veri_inceleme.ipynb` | Aday veri setlerine bakış (sütunlar, etiketler, örnekler) |
| `02_isinma_egitimi.ipynb` | Hattın çalıştığını görmek için ısınma eğitimi (bildiride raporlanmaz) |
| `03_veri_hazirlama.ipynb` | Birleştirme, temizlik, tekilleştirme, sızıntı kontrolü, `veri_birlesik.csv` üretimi |
| `04_anahtar_kelime_filtresi.ipynb` | Anahtar kelime / regex kıyas filtresi |
| `05_…`, `06_…` | Ana eğitim/ölçüm ve çoklu tohum koşuları (son koşular bitince eklenecek) |

Defterler Google Colab için yazıldı (ücretsiz GPU yeterli), açıklamalar Türkçedir.

## Yeniden üretme

- Veri setleri bu depoda **tutulmaz**. `03` defteri açık veri setlerini Hugging Face'ten indirir ve `veri_birlesik.csv` dosyasını kendisi üretir.
- Defterleri Colab'da sırayla çalıştırın (`01` → `06`).
- Burada hiçbir API anahtarı veya kimlik bilgisi kullanılmaz ya da saklanmaz. `.env` dosyalarını ve token'ları asla commit etmeyin (`.gitignore` içindedir).

## Durum

Çalışma sürüyor. Son koşular bitince kesin sonuçlar ve şekiller buraya eklenecek; o zamana kadar sayı iddia edilmiyor.

## Lisans / veri

Yeniden kullanmadan önce her veri setinin lisansını Hugging Face sayfasından kontrol edin.
