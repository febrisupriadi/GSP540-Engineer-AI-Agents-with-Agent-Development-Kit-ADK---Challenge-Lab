# GSP540-Engineer-AI-Agents-with-Agent-Development-Kit-ADK---Challenge-Lab
Dokumentasi ini berisi catatan tahapan penyelesaian tantangan (Challenge Lab) menggunakan Agent Development Kit (ADK) di Google Cloud.

## Challenge Scenario
Bergabung dengan *Cymbal Travel* untuk memperbaiki, mengonfigurasi, dan mendeploy sekumpulan agen AI (Travel Scout, Destination Verifier, dan Brochure Auditor) agar dapat berjalan dengan andal, ter-grounding dengan benar, serta menggunakan struktur data yang konsisten.

You have just joined **Cymbal Travel**, a premier travel agency dedicated to curating the perfect vacation experiences for their customers. Cymbal Travel uses a suite of AI agents to scour the web for travel updates, validate destination data, and audit marketing brochures for accuracy.

Your team has built prototypes for a **"Travel Scout"** and a **"Brochure Auditor"** using Google's **Agent Development Kit (ADK)**. However, the prototypes are currently misconfigured, incomplete, or broken.

For example, the **Brochure Auditor** is supposed to be a multi-agent pipeline that both checks and fixes errors, but the previous engineer only implemented the "check" phase. The **Travel Scout** hasn't been given access to Google Search yet.

As a new Agent Engineer, your job is to repair and deploy these agents to ensure downstream systems receive consistent, accurate data.

You will be working in the `adk_project` directory, which contains:
* `my_google_search_agent`: A "Travel Scout" meant to search for events (currently broken).
* `geo_validator`: A "Destination Verifier" that returns unstructured text (needs a strict schema).
* `llm_auditor`: A sophisticated multi-agent system for brochure auditing (needs configuration).


---

## Task 1. Install ADK and set up your environment
1. **Memperbarui PATH & Menginstal ADK**:
   ```bash
   export PATH=$PATH:"/home/${USER}/.local/bin"
   python3 -m pip install google-adk

2. **Autentikasi Google Cloud**:
Menjalankan perintah gcloud auth application-default login dan memasukkan kode verifikasi untuk menetapkan kredensial proyek serta pengguna.

3. **Mengunduh dan Menyiapkan Berkas Proyek**:

   ```bash
   gcloud storage cp gs://qwiklabs-gcp-01-73ac03e7ee28-bucket/adk_project.zip .
   unzip adk_project.zip
   cd adk_project
   pip install -r requirements.txt

---
## Task 2. Initialize and Configure the Travel Scout

Catatan konfigurasi dan pengujian Travel Scout (`my_google_search_agent`):

1. **Konfigurasi Environment (`.env`)**:
   Menyesuaikan direktori `adk_project/my_google_search_agent` dengan parameter Enterprise dan model `gemini-3.5-flash`:
   ```env
   GOOGLE_GENAI_USE_ENTERPRISE=true
   GOOGLE_CLOUD_PROJECT=qwiklabs-gcp-01-73ac03e7ee28
   GOOGLE_CLOUD_LOCATION=global
   MODEL=gemini-3.5-flash

2. **Mengaktifkan Tool Google Search (agent.py)**:
Menambahkan argumen tools=[google_search] pada definisi agen agar dapat mengakses informasi real-time.

3. **Menjalankan ADK Dev UI & Pengujian**:

   ```bash
   cd ~/adk_project
   adk web --allow_origins "regex:https://.*\.cloudshell\.dev"

4. **Mengakses antarmuka web,.** memilih agen my_google_search_agent, dan menguji kueri terkait event di Tokyo pada 2025 hingga berhasil mendapatkan respons yang ter-grounding dengan Google Search.

