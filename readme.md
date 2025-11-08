# GPT-2 Text Generator

Proyek ini menggunakan model GPT-2 Large dari Hugging Face untuk menghasilkan teks kreatif berdasarkan input prompt. Model ini dapat digunakan untuk berbagai keperluan seperti menulis blog, cerita, atau konten kreatif lainnya.

## 📋 Deskripsi

Program ini memanfaatkan model GPT-2 Large (774M parameter) untuk menghasilkan teks secara otomatis. Dengan memberikan judul atau prompt singkat, model akan melanjutkan teks tersebut menjadi paragraf yang koheren dan relevan.

## 🚀 Fitur

- **Text Generation**: Menghasilkan teks kreatif berdasarkan prompt input
- **Multiple Outputs**: Dapat menghasilkan 3 variasi teks sekaligus
- **Customizable Parameters**: Kontrol suhu, sampling, dan panjang output
- **No Repetition**: Mencegah pengulangan kata (n-gram) dalam output

## 📦 Dependencies

```bash
pip install tensorflow
pip install transformers
```

## 🔧 Instalasi

1. Clone atau download repository ini
2. Install dependencies yang diperlukan:
```bash
pip install tensorflow transformers
```

3. Pastikan Anda memiliki koneksi internet untuk download model pertama kali

## 💻 Penggunaan

```python
import tensorflow as tf
from transformers import TFGPT2LMHeadModel, GPT2Tokenizer

# Inisialisasi tokenizer dan model
tokenizer = GPT2Tokenizer.from_pretrained("gpt2-large")
tokenizer.pad_token = tokenizer.eos_token

model = TFGPT2LMHeadModel.from_pretrained(
    "gpt2-large",
    pad_token_id=tokenizer.eos_token_id,
    from_pt=True
)

# Input teks
blog_title = "Weekend Getaway"

# Encode input
input_ids = tokenizer.encode(blog_title, return_tensors='tf')

# Generate teks
output = model.generate(
    input_ids,
    max_length=100,
    temperature=0.9,
    do_sample=True,
    top_p=0.9,
    num_return_sequences=3,
    no_repeat_ngram_size=2,
    early_stopping=True
)

# Decode dan tampilkan hasil
generated_text = tokenizer.decode(output[0], skip_special_tokens=True)
print(generated_text)
```

## ⚙️ Parameter Configuration

| Parameter | Nilai | Deskripsi |
|-----------|-------|-----------|
| `max_length` | 100 | Panjang maksimal teks yang dihasilkan (dalam token) |
| `temperature` | 0.9 | Kontrol keacakan output (0.0-1.0, semakin tinggi semakin kreatif) |
| `do_sample` | True | Mengaktifkan sampling untuk hasil yang lebih variatif |
| `top_p` | 0.9 | Nucleus sampling - hanya memilih token dengan probabilitas kumulatif 90% |
| `num_return_sequences` | 3 | Jumlah variasi teks yang dihasilkan |
| `no_repeat_ngram_size` | 2 | Mencegah pengulangan n-gram (dalam hal ini bigram) |
| `early_stopping` | True | Menghentikan generasi saat mencapai token akhir |

## 📊 Contoh Output

**Input:**
```
Weekend Getaway
```

**Output:**
```
Weekend Getaway

Weekends are the best! You can stay at the hotel, play a little tennis, 
or just go to the beach, the ocean, and some of the other local attractions.
It's all free, it's clean, you can do it on your own time (you just need 
to get a room key), and if you have some time off, there are plenty of 
things you'll love to do.
```

## ⚠️ Catatan Penting

1. **Model Size**: GPT-2 Large memiliki ukuran ~3.25GB. Download pertama kali akan memakan waktu tergantung kecepsi internet Anda.

2. **Deprecation Warning**: TensorFlow classes untuk Transformers akan dihapus di versi 5. Disarankan untuk migrasi ke PyTorch atau pin versi Transformers Anda.

3. **Google Colab**: Jika menggunakan Colab dan ingin autentikasi dengan Hugging Face Hub, buat token di [Hugging Face Settings](https://huggingface.co/settings/tokens) dan simpan sebagai secret `HF_TOKEN`.

4. **Resource Requirements**: Model ini membutuhkan memory yang cukup besar. Disarankan menggunakan GPU untuk performa optimal.

## 🛠️ Troubleshooting

### Model Download Lambat
- Gunakan koneksi internet yang stabil
- Jika di Google Colab, pastikan runtime sedang tidak sibuk

### Out of Memory
- Kurangi `max_length`
- Kurangi `num_return_sequences`
- Gunakan model yang lebih kecil (`gpt2-medium` atau `gpt2`)

### Output Tidak Sesuai
- Sesuaikan `temperature` (lebih rendah = lebih deterministik)
- Ubah `top_p` untuk kontrol sampling
- Coba prompt yang lebih spesifik

## 📝 Lisensi

Model GPT-2 dibuat oleh OpenAI dan tersedia melalui Hugging Face dengan lisensi open source.

## 🤝 Kontribusi

Kontribusi, issues, dan feature requests sangat diterima!

## 📚 Referensi

- [Hugging Face Transformers](https://huggingface.co/docs/transformers)
- [GPT-2 Paper](https://d4mucfpksywv.cloudfront.net/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)
- [TensorFlow](https://www.tensorflow.org/)

---

**Dibuat dengan ❤️ menggunakan GPT-2 dan Transformers**