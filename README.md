# MASTER DATA - MODULAR STRUCTURE

## 📁 Struktur File

```
master_data_sections/
├── 00_metadata.json              # Koordinasi & info struktur
├── 01_personal_info.json         # Info personal & kontak
├── 02_summary.json               # Professional summary
├── 03_experience.json            # Work experiences  
├── 04_education.json             # Pendidikan
├── 05_awards.json                # Penghargaan & kompetisi
├── 06_skills.json                # Technical & personal skills
├── 07_projects.json              # Portfolio projects
├── 08_certificates.json          # Sertifikat
├── 09_organization.json          # Pengalaman organisasi
├── loader.py                     # Load all sections
├── merger.py                     # Merge ke single file
└── README.md                     # File ini
```

## 🎯 Mengapa Modular?

### ✅ Keuntungan

1. **Mudah di-Maintain**
   - Edit satu section tanpa scroll file 2000+ baris
   - Tidak khawatir merusak section lain
   - Cepat menemukan bagian yang ingin diupdate

2. **Lebih Terorganisir**
   - Setiap file punya fokus jelas
   - File size lebih kecil (200-400 baris per file)
   - Easy to review & validate

3. **Fleksibel**
   - Load hanya section yang dibutuhkan
   - Gampang add/update paraphrase angles
   - Git diff lebih readable

4. **Kolaborasi**
   - Bisa dikerjakan parallel (misalnya: update projects & skills bersamaan)
   - Conflict resolution lebih mudah di Git

### ❌ vs Single File

| Aspek | Single File (2149 baris) | Modular (10 files) |
|-------|-------------------------|-------------------|
| Find section | Scroll + search | Buka file langsung |
| Edit | Risk merusak | Isolated |
| Load time | Load all | Load as needed |
| Maintenance | ⚠️ Susah | ✅ Mudah |

## 📝 Cara Penggunaan

### 1. Update Data

**Edit Section Tertentu:**
```bash
# Edit hanya file yang perlu diupdate
nano 03_experience.json    # Update work experience
nano 07_projects.json      # Tambah project baru
nano 06_skills.json        # Update skills
```

**Contoh: Tambah Project Baru**

1. Buka `07_projects.json`
2. Tambah object baru di array:
```json
{
  "id": "proj_006",
  "project_name": "Your New Project",
  "type": "personal/academic/work",
  "description": "...",
  "paraphrase_angles": {
    "ml_focus": "...",
    "nlp_focus": "...",
    // ...
  },
  "technical_stack": [...],
  "semantic_tags": [...],
  "critical_keywords": [...]
}
```
3. Save
4. Done! ✅

### 2. Load Data dalam Python

**Load All Sections:**
```python
from loader import MasterDataLoader

# Initialize loader
loader = MasterDataLoader('master_data_sections/')

# Load all sections
master_data = loader.load_all()

# Access sections
print(master_data['summary'])
print(master_data['projects'])
```

**Load Specific Section:**
```python
# Load hanya yang dibutuhkan
summary = loader.load_section('summary')
projects = loader.load_section('projects')
skills = loader.load_section('skills')
```

**List Available Sections:**
```python
sections = loader.list_sections()
print(sections)
# ['personal_info', 'summary', 'work_experiences', ...]

# Get section info
info = loader.get_section_info('projects')
print(info)
# "Portfolio projects with detailed descriptions and multiple angles"
```

### 3. Merge ke Single File

Jika butuh single file (backup, sharing, compatibility):

```bash
python merger.py

# Output: master_data_merged.json
```

Atau dengan custom output:
```bash
python merger.py master_data_sections master_data_backup.json
```

### 4. Validate JSON

Setelah edit, validate:
```bash
# Validate single file
python3 -m json.tool 07_projects.json > /dev/null && echo "✅ Valid JSON" || echo "❌ Invalid JSON"

# Validate all files
for file in *.json; do
    echo "Checking $file..."
    python3 -m json.tool "$file" > /dev/null && echo "  ✅ Valid" || echo "  ❌ Invalid"
done
```

## 🔍 Isi Setiap Section

### 01_personal_info.json (12 lines)
```json
{
  "full_name": "ARDIYANTO",
  "email": "ardiyanto.ardhiy@gmail.com",
  "phone": "+6281541571692",
  "linkedin": "linkedin.com/in/Ardiyanto",
  "github": "github.com/ardiyanto24",
  "location": "Surakarta, Central Java, Indonesia"
}
```

### 02_summary.json (92 lines)
- `master_components`: Education, experience highlights, strengths, career goals
- `job_focus_variations`: ML Engineer, Data Scientist, NLP Specialist, CV Engineer
- `keyword_pools`: Must-have keywords, conditional keywords
- `tone_variations`: Different tones for different seniority levels

### 03_experience.json (256 lines)
- Work experiences array
- Untuk setiap experience:
  - Job title, company, duration
  - Responsibilities dengan 4-5 paraphrase angles
  - Critical keywords
  - Semantic tags
  - Skills demonstrated

### 04_education.json (48 lines)
- Formal education (S1 Statistics UNS)
- Bootcamps (Bangkit Academy)
- Programs (Rumah Kepemimpinan)

### 05_awards.json (75 lines)
- Competition achievements
- Untuk setiap award:
  - Title, year, role, achievement
  - Description dengan paraphrase angles
  - Skills demonstrated

### 06_skills.json (396 lines)
- **Technical & Analytical Skills**
  - Programming languages (Python, R, SQL)
  - ML/AI Frameworks (TensorFlow, PyTorch, Scikit-learn)
  - NLP Tools (Hugging Face, NLTK)
  - CV Tools (OpenCV, YOLO)
  - Data tools (Pandas, NumPy, Matplotlib)
  - Cloud & deployment (GCP)
- **Personal Strengths**
  - Soft skills dengan evidence

### 07_projects.json (130 lines)
- Portfolio projects (5 main projects)
- Untuk setiap project:
  - Name, type, description
  - Technical stack
  - Key challenges & solutions
  - Paraphrase angles (NLP focus, DL focus, engineering focus, etc.)
  - Semantic tags
  - Outcomes & impact

### 08_certificates.json (8 lines)
- Professional certifications
- Online courses (Coursera, Google, DeepLearning.AI)
- Relevance keywords

### 09_organization.json (175 lines)
- Organization experiences (3 positions)
- Untuk setiap role:
  - Organization, position, duration
  - Responsibilities dengan paraphrase angles
  - Skills demonstrated
  - Achievements

## 🛠️ Maintenance Tips

### Weekly Update Checklist
```
□ Ada project baru? → Update 07_projects.json
□ Belajar skill/tech baru? → Update 06_skills.json
□ Selesai course? → Update 08_certificates.json
□ Ada achievement baru? → Update 05_awards.json
□ Review paraphrase angles - tambah variasi jika perlu
```

### Best Practices

1. **Consistency**: Ikuti format yang sudah ada
2. **Paraphrase Angles**: Minimal 4 angles per item (ml_focus, nlp_focus, technical_depth, impact_focus)
3. **Semantic Tags**: Tag dengan comprehensive terms untuk semantic retrieval
4. **Keywords**: Mark critical keywords yang MUST appear di CV
5. **Evidence**: Semua claim harus bisa diverifikasi (no hallucination)

### Git Workflow

```bash
# Before editing
git pull origin main

# Edit specific section
nano 07_projects.json

# Validate
python3 -m json.tool 07_projects.json > /dev/null

# Commit (clear message)
git add 07_projects.json
git commit -m "Add new project: AI Chatbot with RAG"

# Push
git push origin main
```

## 🚀 Integration dengan AI Agent

### Cara AI Agent Load Data

```python
# In AI Agent code (src/utils/master_data_loader.py)

from master_data_sections.loader import MasterDataLoader

class AIAgentMasterDataLoader:
    def __init__(self):
        self.loader = MasterDataLoader('data/master_data_sections/')
    
    def load(self):
        """Load all master data"""
        return self.loader.load_all()
    
    def get_section(self, section_name):
        """Load specific section only"""
        return self.loader.load_section(section_name)
```

### Performance

- **Before (Single file)**: Load entire 2149 lines every time
- **After (Modular)**: Load only needed sections
  - Example: Hanya butuh projects → load 130 lines saja

### Compatibility

100% compatible dengan AI Agent yang sudah didesain. Structure data sama, hanya cara load yang berbeda.

## 📊 Statistics

| Metric | Value |
|--------|-------|
| Original file | 2149 lines |
| Total modular files | 10 files |
| Avg lines per file | ~200-400 lines |
| Largest file | 06_skills.json (396 lines) |
| Smallest file | 08_certificates.json (8 lines) |
| Metadata file | 00_metadata.json (53 lines) |

## ❓ FAQ

**Q: Apakah harus load semua files?**  
A: Tidak! Bisa load hanya section yang dibutuhkan.

**Q: Bagaimana kalau butuh single file lagi?**  
A: Jalankan `python merger.py` untuk generate merged file.

**Q: Apakah format/structure berubah?**  
A: Tidak! Content 100% sama, hanya di-split ke multiple files.

**Q: Apa yang berubah di AI Agent code?**  
A: Hanya bagian load data. Gunakan `loader.py` instead of `json.load()`.

**Q: Bagaimana backup?**  
A: Backup seluruh folder `master_data_sections/` (Git recommended).

**Q: Kalau ada error di satu file?**  
A: Hanya satu section affected. Other sections tetap aman.

**Q: Bisa edit manual di text editor?**  
A: Yes! File format JSON biasa, bisa edit pakai nano/vim/VSCode/etc.

## 🔧 Troubleshooting

### Error: "JSONDecodeError"
```bash
# Validate file
python3 -m json.tool 07_projects.json

# Common issues:
# - Missing comma
# - Trailing comma before }
# - Unescaped quotes in strings
```

### Error: "Section not found"
```python
# Check available sections
loader = MasterDataLoader('master_data_sections/')
print(loader.list_sections())

# Check metadata
cat 00_metadata.json
```

### File tidak muncul di loader
```bash
# Check file naming
ls -la master_data_sections/

# Must match pattern in 00_metadata.json
cat 00_metadata.json | grep section_files
```

## 📞 Support

Kalau ada pertanyaan atau issue:
1. Check README ini dulu
2. Validate JSON: `python3 -m json.tool <file>`
3. Check loader code: `loader.py`
4. Review metadata: `00_metadata.json`

---

**Last Updated**: 2026-01-31  
**Version**: 2.0_modular  
**Owner**: Ardiyanto  
**Total Sections**: 9  
**Total Files**: 10 (9 sections + 1 metadata)
