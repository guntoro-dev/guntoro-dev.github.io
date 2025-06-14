<!-- Chosen Palette: Nuansa Netral Hangat dengan Aksen Biru Lembut (Warm Neutral with Soft Blue Accents) -->
<!-- Application Structure Plan: Aplikasi ini dirancang sebagai Single-Page Application (SPA) dengan struktur dua kolom utama: sidebar navigasi di kiri dan area konten dinamis di kanan. Struktur ini dipilih untuk kemudahan navigasi antar bagian profil (Home, Tentang Saya, Pengalaman, Pendidikan, Keahlian, Kontak) tanpa memuat ulang halaman. Interaksi utama adalah klik pada item navigasi yang akan menampilkan bagian konten yang sesuai dan menyembunyikan yang lain, menciptakan alur pengguna yang intuitif dan cepat untuk menjelajahi seluruh informasi profil secara linear atau melompat antar bagian. -->
<!-- Visualization & Content Choices: Semua informasi profil (ringkasan, pengalaman, pendidikan, keahlian, kontak) disajikan dalam format teks terstruktur (paragraf, daftar, poin-poin) dalam section terpisah. Goalnya adalah menginformasikan dan membandingkan (antar pengalaman/skill). Metode presentasi ini dipilih karena paling efektif dan efisien untuk data resume kualitatif dan tekstual. Tidak ada data kuantitatif yang memerlukan visualisasi Chart.js atau Plotly.js dalam laporan sumber ini. Interaksi yang ada adalah navigasi antar section. Tidak ada grafik SVG atau Mermaid JS yang digunakan. Ikon menggunakan karakter Unicode/HTML terstruktur. -->
<!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Profil Sarjuni Guntoro Saputra</title>
    <script src="[https://cdn.tailwindcss.com](https://cdn.tailwindcss.com)"></script>
    <style>
        @import url('[https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap](https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap)');
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f7f7f7;
            color: #333;
        }
        .sidebar {
            background-color: #2c3e50; /* Darker neutral */
            color: #ecf0f1;
            box-shadow: 2px 0 8px rgba(0,0,0,0.2);
            transition: transform 0.3s ease-in-out;
            z-index: 1000;
        }
        .sidebar-item {
            padding: 1rem 1.5rem;
            cursor: pointer;
            transition: background-color 0.2s ease;
        }
        .sidebar-item:hover {
            background-color: #34495e; /* Slightly lighter dark neutral */
        }
        .sidebar-item.active {
            background-color: #3498db; /* Soft blue accent */
            font-weight: 600;
        }
        .main-content {
            background-color: #ffffff; /* Light neutral */
            min-height: 100vh;
            transition: margin-left 0.3s ease-in-out;
        }
        .hero-section {
            background-image: url('[https://picsum.photos/id/1040/1920/1080](https://picsum.photos/id/1040/1920/1080)'); /* Cool abstract nature background */
            background-size: cover;
            background-position: center;
            height: 60vh;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.7);
            border-radius: 0.75rem;
            margin: 1.5rem;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }
        .profile-photo {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            object-fit: cover;
            border: 4px solid #ffffff;
            box-shadow: 0 0 15px rgba(0,0,0,0.3);
        }
        @media (max-width: 768px) {
            .sidebar {
                transform: translateX(-100%);
                position: fixed;
                height: 100%;
                width: 250px;
            }
            .sidebar.open {
                transform: translateX(0);
            }
            .main-content {
                margin-left: 0;
            }
            .menu-button {
                display: block;
            }
        }
    </style>
</head>
<body class="flex flex-col md:flex-row">
    <!-- Tombol Menu untuk Mobile -->
    <button id="menuButton" class="md:hidden fixed top-4 left-4 p-3 bg-blue-500 text-white rounded-full shadow-lg z-[1001]">
        ☰
    </button>

    <!-- Sidebar -->
    <nav id="sidebar" class="sidebar flex flex-col w-64 md:w-64 flex-shrink-0 min-h-screen pt-16 md:pt-0">
        <div class="p-6 flex flex-col items-center">
            <img src="[https://placehold.co/120x120/4A90E2/FFFFFF?text=SG](https://placehold.co/120x120/4A90E2/FFFFFF?text=SG)" alt="Sarjuni Guntoro Saputra" class="profile-photo mb-4">
            <h1 class="text-2xl font-bold text-center">Sarjuni Guntoro Saputra</h1>
            <p class="text-sm text-gray-400 text-center">Analisis Sistem | Dukungan Teknis</p>
        </div>
        <ul class="flex flex-col flex-grow">
            <li class="sidebar-item active" data-section="home">
                <span class="mr-3">🏠</span> Beranda
            </li>
            <li class="sidebar-item" data-section="about">
                <span class="mr-3">👤</span> Tentang Saya
            </li>
            <li class="sidebar-item" data-section="experience">
                <span class="mr-3">💼</span> Pengalaman
            </li>
            <li class="sidebar-item" data-section="education">
                <span class="mr-3">🎓</span> Pendidikan
            </li>
            <li class="sidebar-item" data-section="skills">
                <span class="mr-3">🛠️</span> Keahlian
            </li>
            <li class="sidebar-item" data-section="contact">
                <span class="mr-3">📞</span> Kontak
            </li>
        </ul>
    </nav>

    <!-- Main Content -->
    <main id="mainContent" class="main-content flex-grow p-4 md:ml-0 overflow-auto">
        <!-- Section: Home -->
        <section id="home" class="content-section active-section">
            <div class="hero-section rounded-xl shadow-lg flex flex-col items-center justify-center p-8 text-center">
                <h2 class="text-5xl md:text-6xl font-extrabold mb-4 animate-fade-in-up">Sarjuni Guntoro Saputra</h2>
                <p class="text-xl md:text-2xl font-light">Analisis Sistem | Dukungan Teknis</p>
                <p class="mt-4 max-w-2xl text-lg opacity-90">
                    Lulusan Manajemen Informatika dengan spesialisasi dalam sistem analisis dan dukungan teknis.
                </p>
            </div>
            <div class="container mx-auto px-4 py-8">
                <h3 class="text-3xl font-semibold mb-6 text-gray-800 border-b-2 border-blue-400 pb-2">Selamat Datang di Profil Saya</h3>
                <p class="text-lg leading-relaxed text-gray-700">
                    Ini adalah gambaran singkat tentang perjalanan profesional dan keahlian saya. Anda dapat menggunakan navigasi di sebelah kiri untuk menjelajahi berbagai bagian profil ini, mulai dari ringkasan tentang diri saya, detail pengalaman kerja dan proyek, latar belakang pendidikan, hingga daftar keahlian dan cara menghubungi saya. Saya harap Anda menemukan informasi yang Anda cari dan mendapatkan pemahaman yang komprehensif tentang kompetensi dan kontribusi yang dapat saya berikan.
                </p>
            </div>
        </section>

        <!-- Section: Tentang Saya -->
        <section id="about" class="content-section hidden">
            <div class="container mx-auto px-4 py-8">
                <h2 class="text-4xl font-bold mb-6 text-gray-800 border-b-2 border-blue-400 pb-2">Tentang Saya</h2>
                <p class="text-lg leading-relaxed mb-6 text-gray-700">
                    Saya adalah lulusan Manajemen Informatika dengan spesialisasi yang kuat dalam sistem analisis dan dukungan teknis. Sepanjang karir saya, saya telah mengembangkan pengalaman praktis dalam instalasi dan pemeliharaan jaringan, serta pengembangan sistem manajemen yang efisien.
                </p>
                <p class="text-lg leading-relaxed mb-6 text-gray-700">
                    Saya memiliki rekam jejak dalam bekerja secara kolaboratif dalam proyek-proyek IT skala menengah, menunjukkan kemampuan adaptasi dan inisiatif tinggi. Saya terbiasa bekerja di bawah tekanan dengan tenggat waktu yang ketat dan memiliki kemampuan cepat belajar untuk menguasai teknologi baru demi mencapai tujuan organisasi.
                </p>
                <p class="text-lg leading-relaxed text-gray-700">
                    Komitmen saya adalah menghadirkan solusi teknologi yang efektif dan dapat diandalkan, serta terus berkontribusi pada pengembangan sistem yang inovatif dan terukur.
                </p>
            </div>
        </section>

        <!-- Section: Pengalaman -->
        <section id="experience" class="content-section hidden">
            <div class="container mx-auto px-4 py-8">
                <h2 class="text-4xl font-bold mb-6 text-gray-800 border-b-2 border-blue-400 pb-2">Pengalaman</h2>
                <p class="text-lg leading-relaxed mb-8 text-gray-700">
                    Bagian ini merangkum perjalanan profesional saya, termasuk peran di perusahaan dan proyek-proyek penting yang telah saya kerjakan. Ini akan memberikan gambaran tentang tanggung jawab dan pencapaian saya dalam lingkungan IT yang dinamis.
                </p>

                <div class="mb-8 p-6 bg-white rounded-lg shadow-md border border-gray-200">
                    <h3 class="text-2xl font-semibold text-gray-900 mb-2">IT Support</h3>
                    <p class="text-lg text-blue-600 mb-1">Visiontech Indo Graha</p>
                    <p class="text-md text-gray-500 mb-4">Feb 2018 - Des 2019 | Seluruh Indonesia</p>
                    <ul class="list-disc list-inside text-gray-700 space-y-2">
                        <li>Membantu engineer merevisi desain teknis sebelum dikirim ke vendor.</li>
                        <li>Instalasi dan maintenance sistem Access Control dan CCTV di berbagai lokasi klien.</li>
                    </ul>
                </div>

                <div class="mb-8 p-6 bg-white rounded-lg shadow-md border border-gray-200">
                    <h3 class="text-2xl font-semibold text-gray-900 mb-2">Pengalaman Project</h3>
                    <p class="text-lg text-blue-600 mb-1">Kominfo Badung, Bali</p>
                    <p class="text-md text-gray-500 mb-4">Agust 2018 - Nov 2018</p>
                    <ul class="list-disc list-inside text-gray-700 space-y-2">
                        <li>Bekerja sama dengan tim Lintas Fungsi untuk merancang dan mengembangkan sistem manajemen informatika.</li>
                        <li>Instalasi perangkat CCTV, akses kontrol, Wall display (Barco & Unisee), dll.</li>
                        <li>Mengoptimalkan sistem komunikasi internal.</li>
                        <li>Melakukan analisis kebutuhan pengguna dan merancang tata letak kabel serta posisi hardware.</li>
                        <li>Bekerja berdasarkan hasil meeting bersama konsultan IT Kominfo.</li>
                    </ul>
                </div>

                <div class="mb-8 p-6 bg-white rounded-lg shadow-md border border-gray-200">
                    <h3 class="text-2xl font-semibold text-gray-900 mb-2">Proyek Sistem Kasir (Tugas Akhir)</h3>
                    <p class="text-lg text-blue-600 mb-1">Bina Sarana Informatika</p>
                    <p class="text-md text-gray-500 mb-4">Juli 2015 - Juli 2015</p>
                    <ul class="list-disc list-inside text-gray-700 space-y-2">
                        <li>Mengembangkan aplikasi sistem kasir menggunakan Visual Basic.</li>
                        <li>Mengelola data transaksi, laporan penjualan, dan stok barang.</li>
                        <li>Menyimpan data dengan database SQL.</li>
                    </ul>
                </div>
            </div>
        </section>

        <!-- Section: Pendidikan -->
        <section id="education" class="content-section hidden">
            <div class="container mx-auto px-4 py-8">
                <h2 class="text-4xl font-bold mb-6 text-gray-800 border-b-2 border-blue-400 pb-2">Pendidikan</h2>
                <p class="text-lg leading-relaxed mb-8 text-gray-700">
                    Bagian ini menyajikan riwayat pendidikan saya yang telah membentuk dasar pengetahuan dan keahlian saya dalam bidang informatika.
                </p>

                <div class="mb-8 p-6 bg-white rounded-lg shadow-md border border-gray-200">
                    <h3 class="text-2xl font-semibold text-gray-900 mb-2">Universitas Bina Sarana Informatika (BSI)</h3>
                    <p class="text-lg text-blue-600 mb-1">Manajemen Informatika</p>
                    <p class="text-md text-gray-500 mb-4">Sept 2011 - Nov 2015</p>
                    <p class="text-lg text-gray-700">Konsentrasi: Pemrograman Bisnis</p>
                </div>
            </div>
        </section>

        <!-- Section: Keahlian -->
        <section id="skills" class="content-section hidden">
            <div class="container mx-auto px-4 py-8">
                <h2 class="text-4xl font-bold mb-6 text-gray-800 border-b-2 border-blue-400 pb-2">Keahlian</h2>
                <p class="text-lg leading-relaxed mb-8 text-gray-700">
                    Keahlian saya mencakup berbagai aspek dalam pengembangan perangkat lunak, desain, analisis sistem, hingga manajemen basis data dan jaringan komputer.
                </p>

                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <div class="p-6 bg-white rounded-lg shadow-md border border-gray-200">
                        <h3 class="text-xl font-semibold text-gray-900 mb-3">💻 Pemrograman & Pengembangan</h3>
                        <ul class="list-disc list-inside text-gray-700 space-y-1">
                            <li>Visual Basic 6.0</li>
                            <li>C++</li>
                            <li>Delphi</li>
                            <li>Java</li>
                        </ul>
                    </div>
                    <div class="p-6 bg-white rounded-lg shadow-md border border-gray-200">
                        <h3 class="text-xl font-semibold text-gray-900 mb-3">🎨 Desain & Pemasaran</h3>
                        <ul class="list-disc list-inside text-gray-700 space-y-1">
                            <li>UI/UX Design</li>
                            <li>SEO/SEM</li>
                            <li>Marketing</li>
                            <li>AutoCAD</li>
                        </ul>
                    </div>
                    <div class="p-6 bg-white rounded-lg shadow-md border border-gray-200">
                        <h3 class="text-xl font-semibold text-gray-900 mb-3">📊 Sistem & Data</h3>
                        <ul class="list-disc list-inside text-gray-700 space-y-1">
                            <li>Sistem Analisis</li>
                            <li>Manajemen Basis Data</li>
                            <li>Problem Solving</li>
                            <li>Jaringan Komputer</li>
                        </ul>
                    </div>
                </div>

                <div class="mt-8 p-6 bg-white rounded-lg shadow-md border border-gray-200">
                    <h3 class="text-xl font-semibold text-gray-900 mb-3">🗣️ Bahasa</h3>
                    <ul class="list-disc list-inside text-gray-700 space-y-1">
                        <li>Indonesia - Profesional</li>
                        <li>English - Native</li>
                    </ul>
                </div>
            </div>
        </section>

        <!-- Section: Kontak -->
        <section id="contact" class="content-section hidden">
            <div class="container mx-auto px-4 py-8">
                <h2 class="text-4xl font-bold mb-6 text-gray-800 border-b-2 border-blue-400 pb-2">Kontak</h2>
                <p class="text-lg leading-relaxed mb-8 text-gray-700">
                    Jangan ragu untuk menghubungi saya melalui detail di bawah ini. Saya terbuka untuk peluang kolaborasi atau diskusi terkait bidang keahlian saya.
                </p>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="p-6 bg-white rounded-lg shadow-md border border-gray-200 flex items-center">
                        <span class="text-blue-500 text-3xl mr-4">📍</span>
                        <div>
                            <h3 class="text-xl font-semibold text-gray-900">Lokasi</h3>
                            <p class="text-lg text-gray-700">Kota Tangerang, Banten, Indonesia</p>
                        </div>
                    </div>
                    <div class="p-6 bg-white rounded-lg shadow-md border border-gray-200 flex items-center">
                        <span class="text-blue-500 text-3xl mr-4">📧</span>
                        <div>
                            <h3 class="text-xl font-semibold text-gray-900">Email</h3>
                            <p class="text-lg text-gray-700">
                                <a href="mailto:Sarjuni.guntoro.s@gmail.com" class="text-blue-600 hover:underline">Sarjuni.guntoro.s@gmail.com</a>
                            </p>
                        </div>
                    </div>
                    <div class="p-6 bg-white rounded-lg shadow-md border border-gray-200 flex items-center">
                        <span class="text-blue-500 text-3xl mr-4">📱</span>
                        <div>
                            <h3 class="text-xl font-semibold text-gray-900">Telepon</h3>
                            <p class="text-lg text-gray-700">
                                <a href="tel:+6281397089236" class="text-blue-600 hover:underline">081397089236</a>
                            </p>
                        </div>
                    </div>
                    <div class="p-6 bg-white rounded-lg shadow-md border border-gray-200 flex items-center">
                        <span class="text-blue-500 text-3xl mr-4">🔗</span>
                        <div>
                            <h3 class="text-xl font-semibold text-gray-900">Profil Online</h3>
                            <p class="text-lg text-gray-700">
                                <a href="[https://www.linkedin.com/in/769a901a0](https://www.linkedin.com/in/769a901a0)" target="_blank" rel="noopener noreferrer" class="text-blue-600 hover:underline">[LinkedIn.com/in/769a901a0](https://LinkedIn.com/in/769a901a0)</a><br>
                                <a href="[https://github.com/sgs-github](https://github.com/sgs-github)" target="_blank" rel="noopener noreferrer" class="text-blue-600 hover:underline">[Github.com/sgs-github](https://Github.com/sgs-github)</a>
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <script>
        const sections = document.querySelectorAll('.content-section');
        const sidebarItems = document.querySelectorAll('.sidebar-item');
        const menuButton = document.getElementById('menuButton');
        const sidebar = document.getElementById('sidebar');

        // Fungsi untuk menampilkan section yang dipilih
        function displaySection(sectionId) {
            sections.forEach(section => {
                section.classList.add('hidden');
                section.classList.remove('active-section');
            });
            document.getElementById(sectionId).classList.remove('hidden');
            document.getElementById(sectionId).classList.add('active-section');

            sidebarItems.forEach(item => {
                item.classList.remove('active');
            });
            document.querySelector(`.sidebar-item[data-section="${sectionId}"]`).classList.add('active');

            // Sembunyikan sidebar di mobile setelah klik
            if (window.innerWidth <= 768) {
                sidebar.classList.remove('open');
            }
        }

        // Event listener untuk item sidebar
        sidebarItems.forEach(item => {
            item.addEventListener('click', () => {
                const sectionId = item.dataset.section;
                displaySection(sectionId);
            });
        });

        // Event listener untuk tombol menu mobile
        menuButton.addEventListener('click', () => {
            sidebar.classList.toggle('open');
        });

        // Tampilkan section "home" secara default saat halaman dimuat
        document.addEventListener('DOMContentLoaded', () => {
            displaySection('home');
        });
    </script>
</body>
</html>
