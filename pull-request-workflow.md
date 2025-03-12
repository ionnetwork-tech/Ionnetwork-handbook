# Kolaborasi dan Review menggunakan *Pull Request*

Bagian ini berisi tentang proses _Pull Request_ yang berjalan di Ion Network, tata cara dan kesepakatan yang berlaku. 

---
### *Main Cast*

1. **Captain (Pengembang Utama)**
   - Tanggung Jawab:
     * Review kode akhir
     * Pengambilan keputusan strategis
     * Manajemen merge dan release

2. **QA (Quality Assurance)**
   - Tanggung Jawab:
     * Pengujian fungsionalitas
     * Verifikasi kualitas kode
     * Validasi standar mutu

3. **Member (Pengembang)**
   - Tanggung Jawab:
     * Pengembangan fitur
     * Pembuatan cabang
     * Implementasi kode

![](https://i.imgur.com/qNyLVwx.png)

### *Pull Request Manifesto @ Ion Network*

1. Tidak boleh ada proses development di dalam *branch* `develop` atau `master` - kedua *branch* tersebut hanya berfungsi untuk `merge, test & release` fitur yang sudah stabil
2. Segera buat *Pull Request* setelah *branch* dibuat dan *remote push* sudah dilakukan.
3. *Pull Request* akan ditolak apabila ditemukan konflik dalam kode. Pengembang harus menyelesaikan konflik tersebut dan memastikan tidak ada konflik dalam *Pull Request*
4. Lakukan penamaan *branch* sesuai kesepakatan bersama ( lihat Ketentuan *Branching* )
5. *Branch* `hotfix` akan menghasilkan *Pull Request* ke *branch* `master` dan *branch* `develop`
7. Pengembang utama sebaiknya melakukan proses `merge` di repositori lokal. Khusus untuk branch `story` sebaiknya dilakukan *preserve commit history* dengan melakukan proses `git merge --no-ff`. Untuk branch lain silahkan `merge & squash` menggunakan `git merge --squash`
8. Pengembang utama yang memiliki akses *push* ke `master` dan `develop` harus mengatur proses `release` aplikasi dan memungkinkan untuk membuat *branch* `release` dengan beberapa permintaan pekerjaan tambahan sebelum akhirnya akan dilakukan `merge` ke `develop` dan `master`

## 🌿 Strategi Branching dan Integrasi Jira

### Pola Penamaan Cabang

Format: `[tipe]/[nomor-tiket]-[deskripsi-singkat]`

#### Tipe Cabang

1. **Story (`story/`)**
   - Untuk fitur besar atau cerita pengguna
   - Contoh: `story/PROJ-123-user-authentication`
   
2. **Task (`task/`)**
   - Untuk tugas spesifik dalam story
   - Contoh: `task/PROJ-124-login-page-design`

3. **Improvement (`improvement/`)**
   - Untuk peningkatan sistem
   - Contoh: `improvement/PROJ-125-performance-optimization`

4. **Bug (`bugfix/`)**
   - Untuk perbaikan bug
   - Contoh: `bugfix/PROJ-126-session-timeout-issue`

5. **Hotfix (`hotfix/`)**
   - Untuk perbaikan kritis produksi
   - Contoh: `hotfix/PROJ-127-security-patch`

### Aturan Branching

1. Tidak ada pengembangan langsung di `develop` atau `master`
2. Buat Pull Request segera setelah push
3. Selesaikan konflik sebelum merge
4. Gunakan nama cabang sesuai kesepakatan

## 🔀 Alur Kerja Pull Request

### Proses Merge

1. **Story Branch**
   ```bash
   # Preserve commit history
   git merge --no-ff
   ```

2. **Cabang Lain**
   ```bash
   # Squash commits
   git merge --squash
   ```

### Konfigurasi Branch

- `master`: Kode produksi stabil
- `develop`: Integrasi fitur
- `latest`: Pengembangan aktif

## 📝 Panduan Commit

### Format Pesan Commit

```
<tipe>: [PROJ-nomor-tiket] Deskripsi singkat

- Detail perubahan
- Alasan perubahan
```

### Tipe Commit

- `feat:` Fitur baru
- `fix:` Perbaikan bug
- `docs:` Perubahan dokumentasi
- `style:` Formatasi kode
- `refactor:` Refaktoring
- `test:` Penambahan tes
- `chore:` Tugas pemeliharaan

## 🤝 Praktik Terbaik

1. Satu cabang per tiket Jira
2. Commit sering dengan pesan jelas
3. Selalu update dari `develop`
4. Gunakan Pull Request untuk merge
5. Lengkapi deskripsi Pull Request

## 🔗 Integrasi Jira-GitHub

### Transisi Tiket

- Gunakan kata kunci di commit/PR:
  * `PROJ-123 Resolves`
  * `PROJ-123 Fixes`
  * `PROJ-123 Closes`

### Template Pull Request

```markdown
## Deskripsi Perubahan
- Nomor Tiket Jira: PROJ-XXX
- Jenis: [Fitur/Perbaikan/Improvement]

## Lingkup Perubahan
- [ ] Fitur baru
- [ ] Perbaikan bug
- [ ] Perubahan dokumentasi

## Proses Pengujian
- [ ] Tes unit
- [ ] Tes integrasi
- [ ] Dokumentasi diperbarui

## Checklist
- [ ] Mengikuti panduan gaya kode
- [ ] Review kode sendiri
- [ ] Tidak ada konflik
```

- [Git Cheatsheet](https://www.git-tower.com/blog/git-cheat-sheet/)
- [Rewrite Commit History](https://git-scm.com/book/id/v2/Git-Tools-Rewriting-History)
- [Squash Published Commits](https://stackoverflow.com/questions/5667884/how-to-squash-commits-in-git-after-they-have-been-pushed)
- [Dokumentasi Jira](https://www.atlassian.com/software/jira)

