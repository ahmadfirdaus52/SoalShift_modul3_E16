# SoalShift_modul3_E16
# SOAL 1
1. Langkah pertama untuk menyelesaikan soal ini yaitu mengurutkan terlebih dahulu input dari user, disini saya menggunakan Bubble Sort.
2. Selanjutnya membuat fungsi untuk menghitung faktorial nya, dengan cara rekursif (nilai yang sekarang dikalikan nilai sebelumnya).
3. Setelah itu membuat thread dengan syntax seperti berikut `pthread_create(&tid[arr[i]], NULL, &tulis,(void *)&nilai);` tid merupakan thread id, tulis merupakan nama fungsi untuk menghitung faktorial nya, sedangkan nilai merupakan global variabel yang berfungsi sebagai batas yang akan digunakan pada fungsi faktorial.
# SOAL 2
- SERVER PENJUAL

Pada server penjual, menggunakan 1 thread yang berfungsi untuk mencetak stok yang tersedia setiap 5 detik. menggunakan perintah `pthread_create(&nama_thread, NULL, nama_fungsi, NULL);` serta dibuat infinite loop sehingga thread akan tetap mencetak selama server masih berjalan. Kemudian, untuk tetap bisa menjaga jumlah stok bernilai sama pada server penjual maupun server pembeli, maka menggunakan konsep shared memory, yang diakses pada thread tersebut, menggunakan perintah `int shmid = shmget(key, sizeof(int), IPC_CREAT | 0666);` `key_t key = 1234;` `stok = shmat(shmid, NULL, 0);` dan `shmdt(stok);`. Pada main digunakan untuk berkomunikasi dengan client (menggunakan socket pada c) dengan menerima inputan dari client dan menambahkan nilai stok.

- SERVER PEMBELI

Pada  server pembeli, menggunakan 1 thread yang berfungsi menerima inputan dari client serta menambahkan nilai stok ketika server menerima inputan `beli`. Pada server pembeli juga digunakan shared memory untuk tetap bisa menjaga jumlah stok yang bernilai sama pada server penjual maupun server pembeli. Perintah yang digunakan ialah `int shmid = shmget(key, sizeof(int), IPC_CREAT | 0666);` `key_t key = 1234;` `stok = shmat(shmid, NULL, 0);` dan `shmdt(stok);`. Pada main hanya digunakan untuk menjalankan thread dan mengkoneksikan dari client dan server (menggunakan socket pada c).

- CLIENT

Pada client, hanya menggunakan socket dan menerima inputan user, serta mengirimnya ke server yang telah terhubung.

# SOAL 3
Menggunakan 4 thread, yaitu sebagai berikut:
- Thread 1

Thread 1 digunakan untuk menjalankan peran Agmal, dimana WakeUp_Status akan bertambah sebanyak 15 ketika fitur `Agmal Ayo Bangun` dipanggil (bertambahnya nilai ini menggunakan flag, dimana ketika fitur dipanggil, maka flag akan berjalan dan Wake_Status akan bertambah). Selain itu pada thread 1 juga digunakan mutex untuk mengendalikan kasus unik, dimana jika fitur `Iraj Ayo Tidur` sudah dijalankan sebanyak 3 kali, maka mutex akan berjalan, mencetak "Agmal Ayo Bangun disabled 10 s" kemudian thread akan di sleep selama 10 detik. thread 1 akan berjalan dari awal program dijalankan hingga WakeUp_Status bernilai lebih dari 100 atau Spirit_Status bernilai kurang dari sama dengan 0 (flag akan menyala dan thread akan di kill dengan `pthread_kill(nama_thread,SIGKILL);`).

- Thread 2

Thread 2 digunakan untuk menjalankan peran Iraj, dimana Spirit_Status akan berkurang sebanyak 20 ketika fitur `Iraj Ayo Tidur` dipanggil (berkurangnya nilai ini menggunakan flag, dimana ketika fitur dipanggil, maka flag akan berjalan dan Spirit_Status akan berkurang). Selain itu pada thread 1 juga digunakan mutex untuk mengendalikan kasus unik, dimana jika fitur `Agmal Ayo Bangun` sudah dijalankan sebanyak 3 kali, maka mutex akan berjalan, mencetak "Iraj Ayo Tidur disabled 10 s" kemudian thread akan di sleep selama 10 detik. thread 2 akan berjalan dari awal program dijalankan hingga WakeUp_Status bernilai lebih dari 100 atau Spirit_Status bernilai kurang dari sama dengan 0 (flag akan menyala dan thread akan di kill dengan `pthread_kill(nama_thread,SIGKILL);`).

- Thread 3

Thread 3 digunakan untuk menjalankan fungsi `All Status`, dimana thread akan mencetak status kedua variabel ketika flag sudah menyala. Flag akan menyala ketika fitur `All Status` dipanggil. thread 3 juga menggunakan mutex agar fungsi tetap berada pada kondisi infinite loop hingga flag menyala.

- Thread 4

Thread 4 digunakan untuk menerima inputan dari user. Thread ini akan mengaktifkan flag pada masing-masing fitur ketika fitur tersebut dijalankan. Ketika WakeUp_Status bernilai lebih dari sama dengan 100 atau Spirit_Status bernilai kurang dari sama dengan 0, maka thread 4 akan mencetak "Agmal Terbangun, mereka bangun pagi dan berolahraga" ketika WakeUp_Status bernilai lebih dari sama dengan 100 dan akan mencetak "Iraj ikut tidur, dan bangun kesiangan bersama Agmal" ketika Spirit_Status bernilai kurang dari sama dengan 0. Setelah itu thread 4 akan di kill menggunakan perintah `pthread_kill(nama_thread, SIGKILL);`.

# SOAL 4
# SOAL 5
