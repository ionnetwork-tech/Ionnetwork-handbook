# Panduan SCRUM

Bagian ini berisi tentang proses SCRUM yang berjalan di Ion Network, dan penerapannya di sistem kolaborasi yang digunakan

---
### SCRUM @ Ion Network


SCRUM di Ion Network terbagi ke dalam beberapa proses utama

- **_Backlog Refinement_** : Event ini merupakan metode memecah dan mendefinisikan lebih lanjut Produk Backlog menjadi item yang lebih kecil dan lebih akurat untuk memastikan item di bagian atas product siap untuk dilakukan sprint berikutnya.
- **_Sprint Planning_** : Selama Perencanaan Sprint, kami menjawab tiga pertanyaan penting: 

    - Mengapa Sprint ini penting?
    - Apa yang bisa dilakukan dengan Sprint ini?
    - Bagaimana pekerjaan yang dipilih akan diselesaikan?

- **_Sprint_** : Tujuan dari Daily Scrum adalah untuk memeriksa kemajuan menuju Sprint Goal dan menyesuaikan Sprint Backlog seperlunya, menyesuaikan pekerjaan yang direncanakan yang akan datang. Para Developers juga diizinkan untuk menyesuaikan rencana mereka untuk mencapai Sprint Goal di luar Daily Scrum. 
- **_Sprint Review_** : Anggota Tim Scrum menyampaikan hasil dari proses selama Sprint sesuai dengan Sprint Goal yang telah disepakati pada saat Sprint Planning (Demo Session) 
- **_Sprint Retrospect_** : Tujuan utama dari Sprint Retrospective adalah untuk merencanakan cara-cara untuk meningkatkan kualitas dan efektivitas. ini adalah kesempatan untuk memeriksa dan mengadaptasi proses yang telah digunakan Tim untuk membangun peningkatan.

---
### Jira @ Ion Network

Dalam proses menjalankan SCRUM, Ion Network menggunakan sistem kolaborasi yang bernama Azure Devops. Berikut adalah hal hal penting yang harus dipahami dalam penggunaan Azure Devops

**JENIS TASK**

- ***Story*** : pekerjaan terkait fitur yang akan dikembangkan
- ***Task*** : pekerjaan kecil pendukung fitur / pecahan *Story* yang akan dikembangkan
- ***Bug*** : pekerjaan terkait ketidaksesuaian atau kesalahan dalam fitur yang telah dikembangkan
- ***Hotfix*** : adalah *Bug* yang muncul saat sistem telah digunakan ( *in production* ) dan harus segera diselesaikan secepatnya. 
- ***Improvement*** : pekerjaan yang akan memperbagus fitur yang telah dikembangkan

**STATUS TASK**

- ***New*** : cukup jelas
- ***In Progress*** : sedang dalam pengerjaan. pengembang diharapkan mencatat waktu pengerjaan melalui fitur *log time / WorkTime*
- ***Resolved*** : pekerjaan sudah selesai dan bisa dilakukan testing oleh QA pada *staging server* atau *beta distribution platform*
- ***Pending*** : pekerjaan ditunda karena ada faktor penghambat
- ***Feedback*** : terdapat hal yang kurang jelas yang harus ditanyakan, diwajibkan untuk meninggalkan komentar/pertanyaan kepada PM
- ***Re-open*** : pekerjaan tidak lulus hasil uji QA dan membutuhkan perbaikan, diwajibkan untuk meninggalkan komentar terkait perbaikan yang dibutuhkan.
- ***Closed*** : pekerjaan lulus hasil uji QA dan siap untuk digunakan.
- ***Rejected*** : pekerjaan tidak akan dikerjakan karena ada beberapa faktor tertentu.

**PRIORITAS TASK**

- ***P0***
- ***P1***
- ***P2***
- ***P3***

