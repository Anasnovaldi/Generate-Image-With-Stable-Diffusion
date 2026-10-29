# StudioAI: Creating Image with Stable Diffusion

Aplikasi web interaktif untuk generate gambar dari teks (text-to-image) menggunakan model Stable Diffusion, dibangun dengan Streamlit dan dijalankan di Google Colab (GPU T4) melalui tunnel Ngrok.

## Fitur

- Generate gambar dari prompt teks
- Kontrol kualitas lewat parameter Quality Steps, Creativity (CFG), dan Seed
- Negative prompt untuk menghindari elemen yang tidak diinginkan
- Antarmuka web sederhana, tidak perlu coding untuk memakainya

## Teknologi yang Digunakan

### Streamlit
Framework Python untuk membangun antarmuka web interaktif secara cepat, khususnya untuk demo model AI/ML. Cukup ditulis dengan Python biasa tanpa perlu HTML, CSS, atau JavaScript manual.

### Ngrok
Layanan tunneling yang membuat server lokal (yang berjalan di Colab/komputer, biasanya hanya bisa diakses dari `localhost`) dapat diakses secara publik lewat internet melalui URL sementara. Ngrok tidak menyediakan server bersama — setiap pengguna mendapat tunnel pribadi menuju server masing-masing.

## Instalasi

```bash
pip install -q pyngrok streamlit torch diffusers transformers
```

## Cara Mendapatkan Ngrok API Key (Auth Token)

1. Buka [https://ngrok.com](https://ngrok.com) dan buat akun gratis (bisa daftar pakai email atau akun Google/GitHub)
2. Setelah login, masuk ke **Dashboard**
3. Di sidebar kiri, klik menu **"Your Authtoken"** (di bawah bagian "Getting Started")
4. Salin token yang muncul di sana (bentuknya deretan huruf dan angka panjang)
5. **Jangan taruh token ini langsung di kode!** Simpan lewat Colab Secrets:
   - Klik ikon gembok 🔑 di sidebar kiri Google Colab
   - Tambahkan secret baru dengan nama `NGROK_TOKEN`, isi dengan token kamu
   - Panggil di kode dengan:
     ```python
     from google.colab import userdata
     auth_token = userdata.get('NGROK_TOKEN')
     ```

## Cara Menjalankan

1. Jalankan seluruh cell notebook secara berurutan di Google Colab (pastikan runtime GPU aktif: `Runtime > Change runtime type > T4 GPU`)
2. Setelah cell terakhir dijalankan, akan muncul URL publik ngrok (contoh: `https://xxxxx.ngrok-free.dev`)
3. Buka URL tersebut di browser untuk mengakses aplikasi
4. Masukkan prompt dan negative prompt, atur parameter di sidebar, lalu klik **Initialize Generation**

## Parameter

| Parameter | Fungsi |
|---|---|
| **Quality Steps** | Jumlah iterasi proses denoising. Makin tinggi, makin detail hasilnya, tapi makin lama prosesnya |
| **Creativity (CFG)** | Seberapa ketat model mengikuti prompt. Rendah = lebih bebas/artistik, tinggi = lebih patuh ke instruksi |
| **Seed Control** | Angka kunci untuk pola noise awal. Seed yang sama + prompt yang sama = hasil gambar yang identik |

## Catatan Penting

Setelah selesai menggunakan aplikasi, **matikan runtime Colab sepenuhnya** (`Runtime > Disconnect and delete runtime`) untuk membebaskan resource GPU dan mematikan tunnel ngrok secara otomatis.

## Model

- [`runwayml/stable-diffusion-v1-5`](https://huggingface.co/runwayml/stable-diffusion-v1-5)