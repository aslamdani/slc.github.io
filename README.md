
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Scientists Learning Center - Aplikasi Bimbingan Belajar Modern</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            blue: '#1E40AF',
                            blueHover: '#1D4ED8',
                            green: '#059669',
                            greenHover: '#047857',
                            lightBg: '#F8FAFC',
                            darkText: '#0F172A'
                        }
                    }
                }
            }
        }
    </script>
    <!-- Font Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        body { font-family: 'Inter', sans-serif; }
        .glassmorphism {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(226, 232, 240, 0.8);
        }
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #CBD5E1;
            border-radius: 9999px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover {
            background: #94A3B8;
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 antialiased flex flex-col min-h-screen">

    <!-- TOPBAR / HEADER -->
    <header class="sticky top-0 z-40 bg-white border-b border-slate-200 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-16">
                <!-- Brand Logo -->
                <div class="flex items-center gap-3">
                    <div class="bg-gradient-to-tr from-blue-700 to-emerald-600 p-2.5 rounded-xl text-white shadow-md shadow-blue-500/20">
                        <i data-lucide="atom" class="w-6 h-6 animate-spin-slow"></i>
                    </div>
                    <div>
                        <h1 class="font-extrabold text-lg sm:text-xl text-slate-900 tracking-tight leading-none">
                            Scientists <span class="text-emerald-600">Learning Center</span>
                        </h1>
                        <p class="text-[11px] font-medium text-slate-500 tracking-wide mt-0.5">Bimbingan Belajar Kurikulum Nasional</p>
                    </div>
                </div>

                <!-- Right Quick Stats & User Profile -->
                <div class="flex items-center gap-4">
                    <div class="hidden md:flex items-center gap-3 bg-slate-100 px-3 py-1.5 rounded-full border border-slate-200 text-xs font-semibold text-slate-600">
                        <span class="flex items-center gap-1.5 text-blue-700">
                            <i data-lucide="award" class="w-4 h-4"></i> Poin: <span id="userPoints">1,250</span>
                        </span>
                        <span class="text-slate-300">|</span>
                        <span class="flex items-center gap-1 text-emerald-600">
                            <i data-lucide="check-circle" class="w-4 h-4"></i> Completed: <span id="completedFormatifs">14/180</span>
                        </span>
                    </div>

                    <div class="flex items-center gap-2 border-l border-slate-200 pl-4">
                        <div class="w-9 h-9 rounded-full bg-blue-100 text-blue-800 flex items-center justify-center font-bold text-sm border-2 border-blue-500">
                            AH
                        </div>
                        <div class="hidden sm:block text-left text-xs">
                            <div class="font-bold text-slate-800">Ahmad Hidayat</div>
                            <div class="text-slate-500" id="userRoleBadge">Siswa SMA 10</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <!-- LEVEL & SUBJECT FILTER BAR -->
    <section class="bg-gradient-to-r from-blue-900 via-blue-800 to-emerald-800 text-white shadow-md">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4">
            <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
                
                <!-- Level Switcher -->
                <div class="flex items-center gap-1.5 overflow-x-auto pb-1 md:pb-0 custom-scrollbar">
                    <span class="text-xs font-semibold uppercase text-blue-200 mr-2 flex items-center gap-1">
                        <i data-lucide="layers" class="w-3.5 h-3.5"></i> Tingkat:
                    </span>
                    <button onclick="changeLevel('SD')" id="btn-SD" class="level-btn px-3 py-1.5 rounded-lg text-xs font-bold transition-all bg-white/10 hover:bg-white/20 text-white">SD (1-6)</button>
                    <button onclick="changeLevel('SMP')" id="btn-SMP" class="level-btn px-3 py-1.5 rounded-lg text-xs font-bold transition-all bg-white/10 hover:bg-white/20 text-white">SMP (7-9)</button>
                    <button onclick="changeLevel('SMA')" id="btn-SMA" class="level-btn px-3 py-1.5 rounded-lg text-xs font-bold transition-all bg-emerald-500 text-white shadow">SMA (10-12)</button>
                </div>

                <!-- Class Dropdown & Semester Toggle -->
                <div class="flex items-center gap-3">
                    <div class="flex items-center gap-2">
                        <label for="classSelect" class="text-xs text-blue-100 font-medium">Kelas:</label>
                        <select id="classSelect" onchange="updateClassFilter()" class="bg-white text-slate-900 font-semibold text-xs rounded-lg px-3 py-1.5 border border-white/30 focus:outline-none focus:ring-2 focus:ring-emerald-400 shadow-sm cursor-pointer">
                            <!-- Populated dynamically -->
                        </select>
                    </div>

                    <div class="bg-white/10 p-0.5 rounded-lg border border-white/20 flex text-xs">
                        <button onclick="changeSemester(1)" id="sem-1-btn" class="px-3 py-1 rounded-md font-semibold transition-all bg-white text-blue-900 shadow">Semester 1</button>
                        <button onclick="changeSemester(2)" id="sem-2-btn" class="px-3 py-1 rounded-md font-semibold transition-all text-white hover:bg-white/10">Semester 2</button>
                    </div>
                </div>
            </div>

            <!-- Subject Badges Slider -->
            <div class="mt-4 pt-3 border-t border-white/10">
                <div class="text-xs text-blue-200 mb-2 font-medium flex items-center justify-between">
                    <span><i data-lucide="book-open" class="w-3.5 h-3.5 inline mr-1"></i> Pilih Mata Pelajaran Kurikulum Nasional:</span>
                    <span id="activeSubjectDisplay" class="font-bold text-emerald-300">Matematika</span>
                </div>
                <div id="subjectContainer" class="flex gap-2 overflow-x-auto pb-2 custom-scrollbar">
                    <!-- Dynamic Subjects Rendered Here -->
                </div>
            </div>
        </div>
    </section>

    <!-- CORE MODULE TABS -->
    <div class="bg-white border-b border-slate-200 sticky top-16 z-30 shadow-xs">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <nav class="flex space-x-2 sm:space-x-8 overflow-x-auto custom-scrollbar" aria-label="Tabs">
                <button onclick="switchTab('materi')" id="tab-materi" class="tab-btn border-emerald-600 text-emerald-600 py-3 px-1 border-b-2 font-bold text-xs sm:text-sm flex items-center gap-2 whitespace-nowrap">
                    <i data-lucide="book-open-text" class="w-4 h-4"></i> 1. Materi & Rangkuman
                </button>
                <button onclick="switchTab('evaluasi')" id="tab-evaluasi" class="tab-btn border-transparent text-slate-500 hover:text-slate-700 hover:border-slate-300 py-3 px-1 border-b-2 font-bold text-xs sm:text-sm flex items-center gap-2 whitespace-nowrap">
                    <i data-lucide="clipboard-check" class="w-4 h-4"></i> 2. Evaluasi & Asesmen (Formatif)
                </button>
                <button onclick="switchTab('interaksi')" id="tab-interaksi" class="tab-btn border-transparent text-slate-500 hover:text-slate-700 hover:border-slate-300 py-3 px-1 border-b-2 font-bold text-xs sm:text-sm flex items-center gap-2 whitespace-nowrap">
                    <i data-lucide="messages-square" class="w-4 h-4"></i> 3. Interaksi & Dukungan Belajar
                </button>
                <button onclick="switchTab('manajemen')" id="tab-manajemen" class="tab-btn border-transparent text-slate-500 hover:text-slate-700 hover:border-slate-300 py-3 px-1 border-b-2 font-bold text-xs sm:text-sm flex items-center gap-2 whitespace-nowrap">
                    <i data-lucide="bar-chart-3" class="w-4 h-4"></i> 4. Manajemen & Rapor
                </button>
            </nav>
        </div>
    </div>

    <!-- MAIN CONTENT CONTAINER -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 flex-1 w-full">

        <!-- MODULE 1: MATERI & RANGKUMAN -->
        <section id="module-materi" class="module-section space-y-6">
            <!-- Header Info -->
            <div class="bg-gradient-to-r from-blue-50 to-emerald-50 rounded-2xl p-6 border border-blue-100 flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
                <div>
                    <div class="inline-flex items-center gap-2 bg-emerald-100 text-emerald-800 text-xs font-bold px-2.5 py-1 rounded-full mb-2">
                        <i data-lucide="sparkles" class="w-3.5 h-3.5"></i> Kurikulum Nasional Aligned
                    </div>
                    <h2 class="text-xl sm:text-2xl font-extrabold text-slate-900" id="materiHeaderTitle">Rangkuman Materi: Matematika (SMA 10 - Semester 1)</h2>
                    <p class="text-xs sm:text-sm text-slate-600 mt-1">Disusun lengkap sesuai standar kompetensi lulusan terkini tanpa ikatan tahun ajaran spesifik.</p>
                </div>
                <div class="flex gap-2 w-full md:w-auto">
                    <button onclick="downloadPdfSummary()" class="flex-1 md:flex-initial bg-blue-700 hover:bg-blue-800 text-white text-xs font-bold px-4 py-2.5 rounded-xl flex items-center justify-center gap-2 transition-all shadow-sm">
                        <i data-lucide="download" class="w-4 h-4"></i> Download Modul PDF
                    </button>
                    <button onclick="printSummary()" class="bg-white text-slate-700 hover:bg-slate-100 border border-slate-200 text-xs font-bold px-3 py-2.5 rounded-xl flex items-center justify-center gap-2 transition-all">
                        <i data-lucide="printer" class="w-4 h-4"></i> Print
                    </button>
                </div>
            </div>

            <!-- Video/Audio Explainer Component -->
            <div class="bg-slate-900 rounded-2xl p-4 sm:p-6 text-white shadow-xl flex flex-col lg:flex-row gap-6 items-center">
                <div class="w-full lg:w-1/2 aspect-video bg-slate-800 rounded-xl overflow-hidden relative border border-slate-700 flex items-center justify-center group cursor-pointer" onclick="togglePlayVideo()">
                    <div class="absolute inset-0 bg-cover bg-center opacity-40 group-hover:opacity-60 transition-all" style="background-image: url('https://images.unsplash.com/photo-1635070041078-e363dbe005cb?q=80&w=800&auto=format&fit=crop');"></div>
                    <div class="w-14 h-14 rounded-full bg-emerald-500 text-white flex items-center justify-center shadow-lg transform group-hover:scale-110 transition-all z-10">
                        <i data-lucide="play" class="w-6 h-6 fill-current ml-1"></i>
                    </div>
                    <span class="absolute bottom-3 left-3 bg-slate-900/80 backdrop-blur text-[11px] px-2.5 py-1 rounded-md border border-slate-700 text-emerald-400 font-mono">
                        <i data-lucide="video" class="w-3 h-3 inline mr-1"></i> Video Interaktif Tutor Scientists LC
                    </span>
                </div>
                <div class="w-full lg:w-1/2 space-y-3">
                    <span class="text-xs font-bold text-emerald-400 uppercase tracking-widest">Media Audio-Visual</span>
                    <h3 class="text-lg font-bold" id="videoTitle">Penjelasan Konsep Utama & Pemahaman Logika Dasar</h3>
                    <p class="text-slate-300 text-xs sm:text-sm leading-relaxed" id="videoDesc">
                        Simak video pengantar dari Tim Tutor Scientists Learning Center untuk memahami visualisasi konsep secara mendalam sebelum mempelajari modul rangkuman teks.
                    </p>
                    <div class="pt-2 flex items-center gap-4 text-xs text-slate-400">
                        <span class="flex items-center gap-1"><i data-lucide="clock" class="w-3.5 h-3.5"></i> Durasi: 12 Menit</span>
                        <span class="flex items-center gap-1"><i data-lucide="file-badge" class="w-3.5 h-3.5"></i> Tutor Khusus LC</span>
                    </div>
                </div>
            </div>

            <!-- Dynamic Structured Topic Summaries -->
            <div id="materiContentGrid" class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Injected via JavaScript -->
            </div>
        </section>

        <!-- MODULE 2: EVALUASI DAN ASESMEN (FORMATIF) -->
        <section id="module-evaluasi" class="module-section hidden space-y-6">
            <!-- Formatif Selector Header -->
            <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm space-y-4">
                <div class="flex flex-col sm:flex-row justify-between sm:items-center gap-3 border-b border-slate-100 pb-4">
                    <div>
                        <h2 class="text-lg sm:text-xl font-extrabold text-slate-900" id="quizSubjectTitle">Asesmen Formatif: Matematika</h2>
                        <p class="text-xs text-slate-500">Pilih nomor Formatif (1 - 10). Setiap paket berisi 20 soal latihan komprehensif.</p>
                    </div>
                    <div class="flex items-center gap-2 bg-blue-50 text-blue-700 px-3 py-1.5 rounded-lg border border-blue-100 text-xs font-bold">
                        <i data-lucide="help-circle" class="w-4 h-4"></i> Total Soal: 20 Butir / Formatif
                    </div>
                </div>

                <!-- Formatif 1 - 10 Buttons -->
                <div class="flex items-center gap-2 overflow-x-auto pb-1 custom-scrollbar">
                    <span class="text-xs font-bold text-slate-600 mr-1 flex items-center"><i data-lucide="list-checks" class="w-4 h-4 mr-1"></i> Paket:</span>
                    <template id="formatifBtnTemplate">
                        <!-- Cloned via JS -->
                    </template>
                    <div id="formatifButtonsContainer" class="flex gap-2">
                        <!-- Buttons Formatif 1 - 10 generated here -->
                    </div>
                </div>
            </div>

            <!-- Active Quiz Container -->
            <div id="quizContainer" class="bg-white rounded-2xl border border-slate-200 shadow-sm p-6 space-y-6">
                <!-- Quiz Status Bar -->
                <div class="flex flex-wrap items-center justify-between gap-4 bg-slate-50 p-4 rounded-xl border border-slate-200">
                    <div class="flex items-center gap-3">
                        <span class="bg-blue-600 text-white font-extrabold text-xs px-3 py-1.5 rounded-lg" id="currentQuizNumberBadge">Formatif 1</span>
                        <span class="text-slate-700 text-xs sm:text-sm font-semibold">Soal <span id="currentQuestionNum">1</span> dari 20</span>
                    </div>
                    <div class="flex items-center gap-4 text-xs font-bold">
                        <span class="text-slate-500 flex items-center gap-1">
                            <i data-lucide="timer" class="w-4 h-4 text-blue-600"></i> Waktu Sisa: <span id="quizTimer" class="font-mono text-slate-800 text-sm">30:00</span>
                        </span>
                    </div>
                </div>

                <!-- Question Text -->
                <div class="space-y-4">
                    <div class="text-base sm:text-lg font-bold text-slate-900 leading-relaxed" id="questionText">
                        Memuat pertanyaan...
                    </div>

                    <!-- Multiple Choice Options -->
                    <div class="grid grid-cols-1 gap-3 pt-2" id="optionsContainer">
                        <!-- Options A, B, C, D, E injected here -->
                    </div>
                </div>

                <!-- Quiz Navigation Controls -->
                <div class="flex justify-between items-center pt-4 border-t border-slate-100">
                    <button onclick="prevQuestion()" id="btnPrevQue" class="px-4 py-2 rounded-xl text-xs font-bold bg-slate-100 hover:bg-slate-200 text-slate-700 disabled:opacity-50 flex items-center gap-1">
                        <i data-lucide="chevron-left" class="w-4 h-4"></i> Sebelumnya
                    </button>
                    <span class="text-xs text-slate-400 font-medium">Klik opsi untuk menyimpan jawaban</span>
                    <button onclick="nextQuestion()" id="btnNextQue" class="px-5 py-2 rounded-xl text-xs font-bold bg-emerald-600 hover:bg-emerald-700 text-white flex items-center gap-1 shadow-md shadow-emerald-600/20">
                        Berikutnya <i data-lucide="chevron-right" class="w-4 h-4"></i>
                    </button>
                </div>

                <!-- Question Grid Quick Navigator -->
                <div class="pt-4 border-t border-slate-100">
                    <div class="text-xs font-semibold text-slate-500 mb-2">Navigasi Lembar Jawaban (20 Soal):</div>
                    <div class="grid grid-cols-10 sm:grid-cols-20 gap-1.5" id="questionGridNav">
                        <!-- 20 mini buttons generated dynamically -->
                    </div>
                </div>

                <!-- Submit Quiz Button -->
                <div class="text-center pt-2">
                    <button onclick="submitQuiz()" class="bg-gradient-to-r from-blue-700 to-emerald-600 hover:from-blue-800 hover:to-emerald-700 text-white font-extrabold text-xs sm:text-sm px-8 py-3 rounded-xl shadow-lg transition-all transform active:scale-95">
                        <i data-lucide="send" class="w-4 h-4 inline mr-1"></i> Selesaikan & Hitung Nilai Formatif
                    </button>
                </div>
            </div>

            <!-- Quiz Result Modal / Panel (Hidden by Default) -->
            <div id="quizResultPanel" class="hidden bg-white rounded-2xl border border-emerald-200 shadow-xl p-6 space-y-6">
                <div class="text-center space-y-2">
                    <div class="w-16 h-16 rounded-full bg-emerald-100 text-emerald-600 mx-auto flex items-center justify-center">
                        <i data-lucide="award" class="w-10 h-10"></i>
                    </div>
                    <h3 class="text-xl font-extrabold text-slate-900">Hasil Asesmen Formatif</h3>
                    <p class="text-xs text-slate-500">Scientists Learning Center Evaluation Report</p>
                </div>

                <div class="grid grid-cols-2 sm:grid-cols-4 gap-4 text-center">
                    <div class="bg-slate-50 p-3 rounded-xl border border-slate-200">
                        <div class="text-xs text-slate-500">Skor Akhir</div>
                        <div class="text-2xl font-black text-blue-700" id="resultScore">0</div>
                    </div>
                    <div class="bg-slate-50 p-3 rounded-xl border border-slate-200">
                        <div class="text-xs text-slate-500">Benar</div>
                        <div class="text-2xl font-black text-emerald-600" id="resultCorrect">0 / 20</div>
                    </div>
                    <div class="bg-slate-50 p-3 rounded-xl border border-slate-200">
                        <div class="text-xs text-slate-500">Salah</div>
                        <div class="text-2xl font-black text-rose-600" id="resultWrong">0 / 20</div>
                    </div>
                    <div class="bg-slate-50 p-3 rounded-xl border border-slate-200">
                        <div class="text-xs text-slate-500">Status Lulus</div>
                        <div class="text-sm font-bold mt-1.5" id="resultStatus">TUNTAS</div>
                    </div>
                </div>

                <!-- Explanation Section -->
                <div class="space-y-3">
                    <h4 class="font-bold text-sm text-slate-800 flex items-center gap-2">
                        <i data-lucide="book-open" class="w-4 h-4 text-blue-600"></i> Pembahasan Soal Formatif:
                    </h4>
                    <div class="max-h-60 overflow-y-auto custom-scrollbar space-y-2 border border-slate-200 p-3 rounded-xl" id="explanationsList">
                        <!-- Injected JS -->
                    </div>
                </div>

                <div class="flex justify-center gap-3">
                    <button onclick="retryQuiz()" class="bg-slate-800 text-white text-xs font-bold px-6 py-2.5 rounded-xl hover:bg-slate-900 transition">
                        <i data-lucide="rotate-ccw" class="w-3.5 h-3.5 inline mr-1"></i> Coba Ulang Asesmen
                    </button>
                </div>
            </div>
        </section>

        <!-- MODULE 3: INTERAKSI DAN DUKUNGAN BELAJAR -->
        <section id="module-interaksi" class="module-section hidden space-y-6">
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                
                <!-- Left: AI Tutor Study Assistant Chat -->
                <div class="lg:col-span-2 bg-white rounded-2xl border border-slate-200 shadow-sm flex flex-col h-[600px]">
                    <div class="p-4 border-b border-slate-100 bg-gradient-to-r from-blue-900 to-emerald-800 text-white rounded-t-2xl flex items-center justify-between">
                        <div class="flex items-center gap-3">
                            <div class="w-9 h-9 rounded-full bg-emerald-500 text-white flex items-center justify-center font-bold">
                                <i data-lucide="bot" class="w-5 h-5"></i>
                            </div>
                            <div>
                                <h3 class="font-bold text-sm">Scientists AI Tutor Assistant</h3>
                                <p class="text-[11px] text-emerald-200">Siap bantu jawab PR Matematika, Fisika, Kimia, dll. 24/7</p>
                            </div>
                        </div>
                        <span class="bg-emerald-500/20 text-emerald-300 text-[10px] font-bold px-2 py-0.5 rounded border border-emerald-400/30">Online</span>
                    </div>

                    <!-- Chat Messages List -->
                    <div id="chatMessages" class="flex-1 p-4 overflow-y-auto space-y-4 custom-scrollbar bg-slate-50">
                        <div class="flex gap-3">
                            <div class="w-8 h-8 rounded-full bg-emerald-600 text-white flex items-center justify-center text-xs font-bold flex-shrink-0">AI</div>
                            <div class="bg-white p-3.5 rounded-2xl rounded-tl-none border border-slate-200 text-xs sm:text-sm text-slate-700 shadow-xs max-w-[85%]">
                                Halo Ahmad! Saya AI Study Assistant Scientists Learning Center. Ada materi atau soal kesulitan yang ingin didiskusikan hari ini?
                            </div>
                        </div>
                    </div>

                    <!-- Chat Input -->
                    <div class="p-3 bg-white border-t border-slate-200 rounded-b-2xl">
                        <form onsubmit="handleChatSubmit(event)" class="flex gap-2">
                            <input type="text" id="chatInput" placeholder="Tanyakan rumus, teori, atau langkah penyelesaian soal..." class="flex-1 bg-slate-100 border border-slate-200 rounded-xl px-4 py-2.5 text-xs sm:text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500 text-slate-800">
                            <button type="submit" class="bg-emerald-600 hover:bg-emerald-700 text-white px-4 py-2.5 rounded-xl font-bold text-xs flex items-center justify-center transition shadow-md shadow-emerald-600/20">
                                <i data-lucide="send" class="w-4 h-4"></i>
                            </button>
                        </form>
                    </div>
                </div>

                <!-- Right: Schedule Tutor Consultation & Discussion Board -->
                <div class="space-y-6">
                    <!-- Book Session -->
                    <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-5 space-y-4">
                        <h3 class="font-extrabold text-base text-slate-900 flex items-center gap-2 border-b border-slate-100 pb-3">
                            <i data-lucide="calendar" class="w-4 h-4 text-blue-700"></i> Konsultasi Private Tutor
                        </h3>
                        <form onsubmit="handleBookSession(event)" class="space-y-3">
                            <div>
                                <label class="text-xs font-semibold text-slate-600">Pilih Tentor Expertise:</label>
                                <select id="tutorSelect" class="w-full mt-1 bg-slate-50 border border-slate-200 rounded-lg p-2 text-xs focus:ring-2 focus:ring-blue-500">
                                    <option>Dr. Hendra (Spesialis Fisika & Olimpiade Matematika)</option>
                                    <option>Siti Nurhaliza, M.Pd (Pakar Bahasa Arab & Tahsin)</option>
                                    <option>Budi Santoso, S.Si (Tutor Biologi & Kimia SMA)</option>
                                    <option>Ayu Rahmawati, S.Pd (Pakar SD & Tematik IPA/IPS)</option>
                                </select>
                            </div>
                            <div>
                                <label class="text-xs font-semibold text-slate-600">Jadwal Sesi:</label>
                                <input type="datetime-local" required class="w-full mt-1 bg-slate-50 border border-slate-200 rounded-lg p-2 text-xs">
                            </div>
                            <button type="submit" class="w-full bg-blue-700 hover:bg-blue-800 text-white text-xs font-bold py-2.5 rounded-xl transition">
                                Request Sesi Pendampingan
                            </button>
                        </form>
                    </div>

                    <!-- Live Forum Updates -->
                    <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-5 space-y-3">
                        <h3 class="font-extrabold text-base text-slate-900 flex items-center gap-2">
                            <i data-lucide="message-square" class="w-4 h-4 text-emerald-600"></i> Forum Diskusi Siswa LC
                        </h3>
                        <div class="space-y-3 text-xs">
                            <div class="bg-slate-50 p-2.5 rounded-lg border border-slate-200">
                                <div class="font-bold text-slate-800">Tips Hafalan Juz 30 (Tahfidz)</div>
                                <div class="text-slate-500 text-[11px]">Dikirim oleh Rehan (SMP 8) • 12 balasan</div>
                            </div>
                            <div class="bg-slate-50 p-2.5 rounded-lg border border-slate-200">
                                <div class="font-bold text-slate-800">Trik Cepat Logaritma & Eksponen</div>
                                <div class="text-slate-500 text-[11px]">Dikirim oleh Kak Hendra (Tutor) • 28 balasan</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- MODULE 4: MANAJEMEN DAN ADMINISTRASI -->
        <section id="module-manajemen" class="module-section hidden space-y-6">
            <!-- Student Stats Grid -->
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex items-center justify-between">
                    <div>
                        <div class="text-xs font-semibold text-slate-500">Rata-rata Nilai Formatif</div>
                        <div class="text-2xl font-black text-slate-900 mt-1">88.5</div>
                        <span class="text-[11px] text-emerald-600 font-bold">↑ 4.2% bulan ini</span>
                    </div>
                    <div class="p-3 bg-blue-50 text-blue-700 rounded-xl"><i data-lucide="trending-up" class="w-6 h-6"></i></div>
                </div>
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex items-center justify-between">
                    <div>
                        <div class="text-xs font-semibold text-slate-500">Kehadiran Kelas Bimbel</div>
                        <div class="text-2xl font-black text-slate-900 mt-1">96%</div>
                        <span class="text-[11px] text-slate-500">24 dari 25 Sesi</span>
                    </div>
                    <div class="p-3 bg-emerald-50 text-emerald-700 rounded-xl"><i data-lucide="user-check" class="w-6 h-6"></i></div>
                </div>
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex items-center justify-between">
                    <div>
                        <div class="text-xs font-semibold text-slate-500">Materi Selesai</div>
                        <div class="text-2xl font-black text-slate-900 mt-1">32 Bab</div>
                        <span class="text-[11px] text-blue-600 font-bold">Semester 1 & 2</span>
                    </div>
                    <div class="p-3 bg-indigo-50 text-indigo-700 rounded-xl"><i data-lucide="book-marked" class="w-6 h-6"></i></div>
                </div>
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex items-center justify-between">
                    <div>
                        <div class="text-xs font-semibold text-slate-500">Status Pembayaran</div>
                        <div class="text-base font-extrabold text-emerald-600 mt-1">LUNAS</div>
                        <span class="text-[11px] text-slate-400">Aktif s/d Akhir Semester</span>
                    </div>
                    <div class="p-3 bg-emerald-50 text-emerald-700 rounded-xl"><i data-lucide="credit-card" class="w-6 h-6"></i></div>
                </div>
            </div>

            <!-- Detailed Academic Performance & Rapor Bimbel -->
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <!-- Subject Performance Progress Bars -->
                <div class="lg:col-span-2 bg-white rounded-2xl border border-slate-200 shadow-sm p-6 space-y-4">
                    <h3 class="font-extrabold text-slate-900 text-lg border-b border-slate-100 pb-3 flex items-center justify-between">
                        <span><i data-lucide="bar-chart-2" class="w-5 h-5 inline mr-1 text-blue-700"></i> Rekap Evaluasi Formatif Per Pelajaran</span>
                        <span class="text-xs text-slate-500 font-normal">Kurikulum Nasional</span>
                    </h3>
                    
                    <div class="space-y-3" id="adminProgressBars">
                        <!-- Progress Items injected via JS -->
                    </div>
                </div>

                <!-- Rapor Bimbel Generator Widget -->
                <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-6 space-y-4 flex flex-col justify-between">
                    <div class="space-y-3">
                        <div class="w-12 h-12 rounded-xl bg-blue-100 text-blue-800 flex items-center justify-center">
                            <i data-lucide="file-text" class="w-6 h-6"></i>
                        </div>
                        <h3 class="font-extrabold text-slate-900 text-lg">Cetak Rapor Bimbel</h3>
                        <p class="text-xs text-slate-600 leading-relaxed">
                            Unduh Laporan Hasil Belajar (Rapor Asesmen Formatif) resmi bertanda tangan Tim Akademik Scientists Learning Center.
                        </p>
                        <div class="bg-slate-50 p-3 rounded-xl border border-slate-200 text-xs space-y-1.5">
                            <div class="flex justify-between">
                                <span class="text-slate-500">Nama Siswa:</span>
                                <span class="font-bold">Ahmad Hidayat</span>
                            </div>
                            <div class="flex justify-between">
                                <span class="text-slate-500">NIS Bimbel:</span>
                                <span class="font-bold">SLC-2026-889</span>
                            </div>
                            <div class="flex justify-between">
                                <span class="text-slate-500">Predikat:</span>
                                <span class="font-bold text-emerald-600">Sangat Baik (A)</span>
                            </div>
                        </div>
                    </div>
                    <button onclick="generateRapor()" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-bold text-xs py-3 rounded-xl transition shadow-md shadow-emerald-600/20">
                        <i data-lucide="printer" class="w-4 h-4 inline mr-1"></i> Generate & Download Rapor
                    </button>
                </div>
            </div>
        </section>

    </main>

    <!-- FOOTER -->
    <footer class="bg-slate-900 text-slate-400 text-xs border-t border-slate-800 mt-auto">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <div class="flex flex-col md:flex-row justify-between items-center gap-4">
                <div class="flex items-center gap-2">
                    <div class="bg-emerald-500 p-1.5 rounded-lg text-slate-900 font-bold">
                        <i data-lucide="atom" class="w-4 h-4"></i>
                    </div>
                    <span class="font-extrabold text-white text-sm">Scientists Learning Center</span>
                </div>
                <p class="text-center md:text-left">
                    Platform Bimbingan Belajar Kurikulum Nasional Terlengkap SD (1-6), SMP (7-9), SMA (10-12).
                </p>
                <div class="text-slate-500">
                    &copy; Scientists Learning Center. All rights reserved.
                </div>
            </div>
        </div>
    </footer>

    <!-- JAVASCRIPT APPLICATION LOGIC -->
    <script>
        // ==========================================
        // DATA STRUCTURES (Kurikulum Nasional Aligned)
        // ==========================================

        const LEVELS = {
            SD: {
                classes: ['Kelas 1', 'Kelas 2', 'Kelas 3', 'Kelas 4', 'Kelas 5', 'Kelas 6'],
                subjects: ['Matematika', 'IPA', 'IPS', 'PKN', 'B. Indonesia', 'B. Inggris', 'B. Arab', 'Tahfidz', 'Tahsin', 'PJOK', 'Pendidikan Agama Islam']
            },
            SMP: {
                classes: ['Kelas 7', 'Kelas 8', 'Kelas 9'],
                subjects: ['Matematika', 'IPA', 'IPS', 'PKN', 'B. Indonesia', 'B. Inggris', 'B. Arab', 'Tahfidz', 'Tahsin', 'PJOK', 'Pendidikan Agama Islam']
            },
            SMA: {
                classes: ['Kelas 10', 'Kelas 11', 'Kelas 12'],
                subjects: ['Matematika', 'Fisika', 'Kimia', 'Biologi', 'Geografi', 'Sosiologi', 'Ekonomi', 'Sejarah', 'B. Indonesia', 'B. Inggris', 'B. Arab', 'PKN', 'Tahfidz', 'Tahsin', 'PJOK', 'Pendidikan Agama Islam']
            }
        };

        // Current Application State
        let state = {
            currentLevel: 'SMA',
            currentClass: 'Kelas 10',
            currentSemester: 1,
            currentSubject: 'Matematika',
            currentActiveTab: 'materi',
            currentFormatifNum: 1,
            quizState: {
                currentQuestionIndex: 0,
                userAnswers: Array(20).fill(null),
                timerSeconds: 1800, // 30 mins
                timerInterval: null
            }
        };

        // Detailed Content Generators per Subject
        const MATERI_DATABASE = {
            'Matematika': {
                sem1: [
                    { title: 'Persamaan & Pertidaksamaan Nilai Mutlak', desc: 'Pemahaman konsep jarak pada garis bilangan, sifat-sifat nilai mutlak |x|, penyelesaian persamaan linear satu variabel dengan nilai mutlak, serta grafik fungsi mutlak.', formula: '|x| = a ⇔ x = a atau x = -a' },
                    { title: 'Sistem Persamaan Linear Tiga Variabel (SPLTV)', desc: 'Metode eliminasi, substitusi, dan gabungan untuk menyelesaikan masalah kontekstual SPLTV. Aplikasi dalam perhitungan biaya, investasi, dan analisis data.', formula: 'ax + by + cz = d' },
                    { title: 'Fungsi Kuadrat & Grafik Parabola', desc: 'Analisis diskriminan (D = b² - 4ac), titik puncak (x_p = -b/2a, y_p = -D/4a), sumbu simetri, dan penyusunan fungsi kuadrat berdasarkan titik balik.', formula: 'f(x) = ax² + bx + c' }
                ],
                sem2: [
                    { title: 'Trigonometri Dasar & Aturan Sinus/Kosinus', desc: 'Rasio trigonometri sin, cos, tan pada segitiga siku-siku, sudut istimewa (0°, 30°, 45°, 60°, 90°), serta penerapan aturan sinus dan kosinus pada segitiga sembarang.', formula: 'a / sin A = b / sin B = c / sin C' },
                    { title: 'Fungsi Komposisi & Fungsi Invers', desc: 'Operasi aljabar fungsi, konsep (f ∘ g)(x) = f(g(x)), menentukan domain dan kodomain, serta mencari invers fungsi f⁻¹(x).', formula: '(f ∘ g)(x) = f(g(x))' }
                ]
            },
            'Fisika': {
                sem1: [
                    { title: 'Hakikat Fisika & Vektor', desc: 'Metode ilmiah, keselamatan kerja laboratorium, pengukuran besaran pokok & turunan, serta penjumlahan vektor secara analitis & komponen.', formula: 'R = √(F1² + F2² + 2F1F2 cos θ)' },
                    { title: 'Kinematika Gerak Lurus (GLB & GLBB)', desc: 'Analisis perpindahan, kecepatan rata-rata, percepatan konstan, serta gerak jatuh bebas di bawah pengaruh gravitasi bumi.', formula: 'vt = v0 + at ; s = v0 t + ½ at²' }
                ],
                sem2: [
                    { title: 'Hukum Newton tentang Gerak', desc: 'Hukum I, II, dan III Newton, analisis gaya gesek statis/kinetis, gaya normal, serta penerapannya pada bidang miring dan sistem katrol.', formula: 'ΣF = m · a' },
                    { title: 'Usaha dan Energi', desc: 'Konsep usaha w = F · s, energi kinetik, energi potensial gravitasi, dan Hukum Kekekalan Energi Mekanik.', formula: 'EK = ½ mv² ; EP = mgh' }
                ]
            },
            'Kimia': {
                sem1: [
                    { title: 'Struktur Atom & Tabel Periodik', desc: 'Perkembangan teori atom (Dalton hingga Mekanika Kuantum), konfigurasi elektron (Spdf), bilangan kuantum, serta sifat periodik unsur.', formula: 'n, l, m, s (Bilangan Kuantum)' },
                    { title: 'Ikatan Kimia & Gaya Antar Molekul', desc: 'Ikatan ion, ikatan kovalen polar/non-polar, ikatan logam, struktur Lewis, bentuk molekul (VSEPR), dan ikatan hidrogen.', formula: 'Kelektronegatifan ΔEI' }
                ],
                sem2: [
                    { title: 'Stoikiometri & Hukum Dasar Kimia', desc: 'Konsep Mol, massa molar, volume molar gas (STP), Hukum Lavoisier, Proust, Dalton, Gay-Lussac, Avogadro, serta penentuan rumus empiris.', formula: 'Mol (n) = Massa / Ar atau Mr' }
                ]
            },
            'Biologi': {
                sem1: [
                    { title: 'Keanekaragaman Hayati (Biodiversitas)', desc: 'Tingkat keanekaragaman gen, jenis, dan ekosistem di Indonesia. Pembagian wilayah Wallace & Weber serta konservasi in-situ/ex-situ.', formula: 'Klasifikasi Linnaeus' },
                    { title: 'Virus dan Bakteri (Monera)', desc: 'Struktur virus, replikasi litik & lisogenik, peranan eubacteria & archaebacteria dalam kehidupan manusia dan pengolahan pangan.', formula: 'Prokariotik vs Eukariotik' }
                ],
                sem2: [
                    { title: 'Keanekaragaman Protista & Fungi', desc: 'Karakteristik Protista mirip hewan (Protozoa), mirip tumbuhan (Alga), serta klasifikasi jamur (Zygomycota, Ascomycota, Basidiomycota).', formula: 'Simbiosis Mikoriza & Likhen' }
                ]
            },
            'Tahfidz': {
                sem1: [
                    { title: 'Rangkuman Hafalan Juz 30 (Surah An-Naba s/d At-Takwir)', desc: 'Metode murajaah mandiri, tajwid praktis surah-surah pendek, pemahaman maknawiyah tema hari kiamat dan kekuasaan Allah SWT.', formula: 'Metode Tikrar (Pengulangan 40x)' }
                ],
                sem2: [
                    { title: 'Rangkuman Hafalan Juz 30 (Surah Al-Infitar s/d An-Naas)', desc: 'Karakteristik makhraj huruf pada ayat-ayat pendek, penekanan hukum Mad Thabi\'i dan Waqaf Ibtida.', formula: 'Sema\'an Berpasangan' }
                ]
            },
            'Tahsin': {
                sem1: [
                    { title: 'Makhorijul Huruf & Sifatul Huruf', desc: 'Mengenal 5 tempat keluarnya huruf (Al-Jauf, Al-Halq, Al-Lisan, Asy-Syafataim, Al-Khaisyum) dan sifat berlawanan (Hams vs Jahr, Syiddah vs Rakhawah).', formula: 'Tajwid Dasar' }
                ],
                sem2: [
                    { title: 'Hukum Nun Mati / Tanwin & Mim Mati', desc: 'Panduan praktis Izhar Halqi, Idgham Bighunnah/Bilaghunnah, Iqlab, Ikhfa Haqiqi, serta hukum Mim Sujud.', formula: 'Ghunnah 2 Harakat' }
                ]
            }
        };

        // Fallback Generator for other subjects
        function getMateriData(subject, semester) {
            if (MATERI_DATABASE[subject]) {
                return semester === 1 ? MATERI_DATABASE[subject].sem1 : MATERI_DATABASE[subject].sem2;
            }
            return [
                {
                    title: `Konsep Dasar & Teori Utama - ${subject} (Semester ${semester})`,
                    desc: `Pengantar komprehensif materi ${subject} Kurikulum Nasional. Pembahasan mencakup prinsip dasar, definisi istilah kunci, serta integrasi pemahaman konsep secara sistematis.`,
                    formula: `Standar Kompetensi ${subject}`
                },
                {
                    title: `Aplikasi Praktis & Analisis Kasus - ${subject}`,
                    desc: `Studi kasus dan latihan penerapan materi ${subject} dalam kehidupan sehari-hari dan pemecahan masalah kontekstual.`,
                    formula: `Indikator Keberhasilan Belajar`
                }
            ];
        }

        // Dynamic Formatif Questions Generator (20 Questions)
        function generate20Questions(subject, formatifNum, level) {
            const questions = [];
            for (let i = 1; i <= 20; i++) {
                questions.push({
                    id: i,
                    question: `[Soal ${i} - ${subject} Formatif ${formatifNum}] Berdasarkan standar Kurikulum Nasional tingkat ${level}, manakah di bawah ini yang merupakan konsep atau prinsip paling tepat mengenai topik bab ke-${(i % 5) + 1}?`,
                    options: [
                        `Pernyataan A: Merupakan konsep dasar utama yang paling relevan dengan indikator ${i}.`,
                        `Pernyataan B: Merupakan alternatif prinsip pendukung dalam studi ${subject}.`,
                        `Pernyataan C: Merupakan variasi formula khusus yang diterapkan secara kondisional.`,
                        `Pernyataan D: Merupakan hipotesis pembanding yang diuji dalam asesmen ini.`,
                        `Pernyataan E: Merupakan simpulan evaluatif yang berlaku umum.`
                    ],
                    correctIndex: (i + formatifNum) % 5, // Dynamic correct answer
                    explanation: `Pembahasan Soal ${i}: Opsi yang tepat didasarkan pada prinsip utama materi ${subject} Formatif ${formatifNum}. Pemahaman konsep ini sangat krusial untuk menguasai kompetensi dasar yang diuji.`
                });
            }
            return questions;
        }

        // ==========================================
        // INITIALIZATION & EVENT HANDLERS
        // ==========================================

        window.onload = function() {
            lucide.createIcons();
            initLevelButtons();
            renderClassDropdown();
            renderSubjects();
            renderMateriModule();
            renderFormatifButtons();
            initQuiz();
            renderAdminDashboard();
        };

        function switchTab(tabId) {
            state.currentActiveTab = tabId;
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('border-emerald-600', 'text-emerald-600');
                btn.classList.add('border-transparent', 'text-slate-500');
            });
            const activeBtn = document.getElementById(`tab-${tabId}`);
            if (activeBtn) {
                activeBtn.classList.remove('border-transparent', 'text-slate-500');
                activeBtn.classList.add('border-emerald-600', 'text-emerald-600');
            }

            document.querySelectorAll('.module-section').forEach(sec => sec.classList.add('hidden'));
            const targetSection = document.getElementById(`module-${tabId}`);
            if (targetSection) targetSection.classList.remove('hidden');

            lucide.createIcons();
        }

        function changeLevel(level) {
            state.currentLevel = level;
            state.currentClass = LEVELS[level].classes[0];
            state.currentSubject = LEVELS[level].subjects[0];
            
            initLevelButtons();
            renderClassDropdown();
            renderSubjects();
            refreshActiveModuleContent();
        }

        function initLevelButtons() {
            ['SD', 'SMP', 'SMA'].forEach(lvl => {
                const btn = document.getElementById(`btn-${lvl}`);
                if (btn) {
                    if (lvl === state.currentLevel) {
                        btn.className = "level-btn px-3 py-1.5 rounded-lg text-xs font-bold transition-all bg-emerald-500 text-white shadow";
                    } else {
                        btn.className = "level-btn px-3 py-1.5 rounded-lg text-xs font-bold transition-all bg-white/10 hover:bg-white/20 text-white";
                    }
                }
            });
            document.getElementById('userRoleBadge').innerText = `Siswa ${state.currentLevel} (${state.currentClass})`;
        }

        function renderClassDropdown() {
            const select = document.getElementById('classSelect');
            select.innerHTML = '';
            LEVELS[state.currentLevel].classes.forEach(cls => {
                const opt = document.createElement('option');
                opt.value = cls;
                opt.innerText = cls;
                opt.className = "bg-white text-slate-900 font-medium py-1";
                if (cls === state.currentClass) opt.selected = true;
                select.appendChild(opt);
            });
        }

        function updateClassFilter() {
            const select = document.getElementById('classSelect');
            state.currentClass = select.value;
            document.getElementById('userRoleBadge').innerText = `Siswa ${state.currentLevel} (${state.currentClass})`;
            refreshActiveModuleContent();
        }

        function changeSemester(sem) {
            state.currentSemester = sem;
            const btn1 = document.getElementById('sem-1-btn');
            const btn2 = document.getElementById('sem-2-btn');
            if (sem === 1) {
                btn1.className = "px-3 py-1 rounded-md font-semibold transition-all bg-white text-blue-900 shadow";
                btn2.className = "px-3 py-1 rounded-md font-semibold transition-all text-white hover:bg-white/10";
            } else {
                btn2.className = "px-3 py-1 rounded-md font-semibold transition-all bg-white text-blue-900 shadow";
                btn1.className = "px-3 py-1 rounded-md font-semibold transition-all text-white hover:bg-white/10";
            }
            refreshActiveModuleContent();
        }

        function renderSubjects() {
            const container = document.getElementById('subjectContainer');
            container.innerHTML = '';
            const subjects = LEVELS[state.currentLevel].subjects;
            
            subjects.forEach(subj => {
                const btn = document.createElement('button');
                const isActive = subj === state.currentSubject;
                btn.className = `px-3 py-1.5 rounded-xl text-xs font-bold transition-all flex-shrink-0 flex items-center gap-1.5 ${
                    isActive 
                        ? 'bg-emerald-500 text-white shadow-md' 
                        : 'bg-white/10 hover:bg-white/20 text-white'
                }`;
                btn.innerHTML = `<i data-lucide="book" class="w-3.5 h-3.5"></i> ${subj}`;
                btn.onclick = () => {
                    state.currentSubject = subj;
                    renderSubjects();
                    refreshActiveModuleContent();
                };
                container.appendChild(btn);
            });

            document.getElementById('activeSubjectDisplay').innerText = state.currentSubject;
            lucide.createIcons();
        }

        function refreshActiveModuleContent() {
            renderMateriModule();
            renderFormatifButtons();
            initQuiz();
            renderAdminDashboard();
        }

        // ==========================================
        // MODULE 1: MATERI & RANGKUMAN LOGIC
        // ==========================================

        function renderMateriModule() {
            document.getElementById('materiHeaderTitle').innerText = 
                `Rangkuman Materi: ${state.currentSubject} (${state.currentLevel} ${state.currentClass} - Semester ${state.currentSemester})`;
            
            document.getElementById('videoTitle').innerText = `Visualisasi Concept Map: ${state.currentSubject}`;
            document.getElementById('videoDesc').innerText = `Penjelasan mendalam oleh Tim Tutor Experts Scientists Learning Center untuk topik utama ${state.currentSubject} Semester ${state.currentSemester}.`;

            const grid = document.getElementById('materiContentGrid');
            grid.innerHTML = '';

            const list = getMateriData(state.currentSubject, state.currentSemester);

            list.forEach((item, idx) => {
                const card = document.createElement('div');
                card.className = "bg-white p-6 rounded-2xl border border-slate-200 shadow-sm hover:shadow-md transition space-y-3 flex flex-col justify-between";
                card.innerHTML = `
                    <div class="space-y-2">
                        <div class="flex items-center justify-between">
                            <span class="bg-blue-100 text-blue-800 text-[11px] font-extrabold px-2.5 py-1 rounded-lg">Topik Sub-Bab ${idx + 1}</span>
                            <span class="text-xs text-slate-400 font-medium">Kurikulum Nasional</span>
                        </div>
                        <h4 class="font-extrabold text-base text-slate-900">${item.title}</h4>
                        <p class="text-slate-600 text-xs sm:text-sm leading-relaxed">${item.desc}</p>
                    </div>
                    <div class="pt-3 border-t border-slate-100 flex items-center justify-between bg-slate-50 -mx-6 -mb-6 p-4 rounded-b-2xl">
                        <span class="text-xs font-mono text-emerald-700 bg-emerald-50 px-2.5 py-1 rounded border border-emerald-200 font-bold">
                            <i data-lucide="key" class="w-3 h-3 inline mr-1"></i> ${item.formula}
                        </span>
                        <button onclick="downloadPdfSummary()" class="text-xs font-bold text-blue-700 hover:text-blue-900 flex items-center gap-1">
                            Baca Modul <i data-lucide="arrow-right" class="w-3.5 h-3.5"></i>
                        </button>
                    </div>
                `;
                grid.appendChild(card);
            });
            lucide.createIcons();
        }

        function downloadPdfSummary() {
            alert(`[Scientists Learning Center]\nModul Rangkuman PDF untuk ${state.currentSubject} (${state.currentLevel} ${state.currentClass} - Semester ${state.currentSemester}) berhasil di-generate dan siap diunduh!`);
        }

        function printSummary() {
            window.print();
        }

        function togglePlayVideo() {
            alert(`[Scientists LC Player]\nMemutar Video Interaktif Pembahasan ${state.currentSubject}...`);
        }

        // ==========================================
        // MODULE 2: EVALUASI & ASESMEN (FORMATIF 1-10)
        // ==========================================

        function renderFormatifButtons() {
            const container = document.getElementById('formatifButtonsContainer');
            container.innerHTML = '';

            document.getElementById('quizSubjectTitle').innerText = `Asesmen Formatif: ${state.currentSubject} (${state.currentLevel})`;

            for (let i = 1; i <= 10; i++) {
                const btn = document.createElement('button');
                const isActive = i === state.currentFormatifNum;
                btn.className = `px-3.5 py-1.5 rounded-xl text-xs font-extrabold transition-all flex-shrink-0 ${
                    isActive 
                        ? 'bg-blue-700 text-white shadow-md' 
                        : 'bg-slate-100 hover:bg-slate-200 text-slate-700 border border-slate-200'
                }`;
                btn.innerText = `Formatif ${i}`;
                btn.onclick = () => {
                    state.currentFormatifNum = i;
                    renderFormatifButtons();
                    initQuiz();
                };
                container.appendChild(btn);
            }
        }

        let currentQuestionsList = [];

        function initQuiz() {
            state.quizState.currentQuestionIndex = 0;
            state.quizState.userAnswers = Array(20).fill(null);
            currentQuestionsList = generate20Questions(state.currentSubject, state.currentFormatifNum, state.currentLevel);

            document.getElementById('quizResultPanel').classList.add('hidden');
            document.getElementById('quizContainer').classList.remove('hidden');
            document.getElementById('currentQuizNumberBadge').innerText = `Formatif ${state.currentFormatifNum}`;

            renderQuestion();
            renderQuestionGridNav();
        }

        function renderQuestion() {
            const idx = state.quizState.currentQuestionIndex;
            const q = currentQuestionsList[idx];

            document.getElementById('currentQuestionNum').innerText = idx + 1;
            document.getElementById('questionText').innerText = q.question;

            const optionsContainer = document.getElementById('optionsContainer');
            optionsContainer.innerHTML = '';

            const optionPrefixes = ['A', 'B', 'C', 'D', 'E'];

            q.options.forEach((optText, oIdx) => {
                const isSelected = state.quizState.userAnswers[idx] === oIdx;
                const optBtn = document.createElement('button');
                optBtn.className = `w-full text-left p-3.5 rounded-xl border text-xs sm:text-sm font-medium transition flex items-center justify-between ${
                    isSelected 
                        ? 'bg-emerald-50 border-emerald-500 text-emerald-900 font-bold ring-2 ring-emerald-400' 
                        : 'bg-white border-slate-200 hover:bg-slate-50 text-slate-700'
                }`;
                optBtn.innerHTML = `
                    <div class="flex items-center gap-3">
                        <span class="w-6 h-6 rounded-lg ${isSelected ? 'bg-emerald-600 text-white' : 'bg-slate-100 text-slate-600'} flex items-center justify-center font-bold text-xs">
                            ${optionPrefixes[oIdx]}
                        </span>
                        <span>${optText}</span>
                    </div>
                    ${isSelected ? '<i data-lucide="check-circle-2" class="w-4 h-4 text-emerald-600"></i>' : ''}
                `;
                optBtn.onclick = () => selectOption(oIdx);
                optionsContainer.appendChild(optBtn);
            });

            document.getElementById('btnPrevQue').disabled = (idx === 0);
            document.getElementById('btnNextQue').disabled = (idx === 19);

            renderQuestionGridNav();
            lucide.createIcons();
        }

        function selectOption(oIdx) {
            state.quizState.userAnswers[state.quizState.currentQuestionIndex] = oIdx;
            renderQuestion();
        }

        function prevQuestion() {
            if (state.quizState.currentQuestionIndex > 0) {
                state.quizState.currentQuestionIndex--;
                renderQuestion();
            }
        }

        function nextQuestion() {
            if (state.quizState.currentQuestionIndex < 19) {
                state.quizState.currentQuestionIndex++;
                renderQuestion();
            }
        }

        function renderQuestionGridNav() {
            const gridNav = document.getElementById('questionGridNav');
            gridNav.innerHTML = '';

            for (let i = 0; i < 20; i++) {
                const isAnswered = state.quizState.userAnswers[i] !== null;
                const isCurrent = i === state.quizState.currentQuestionIndex;

                const btn = document.createElement('button');
                btn.className = `h-7 text-[11px] font-bold rounded-md flex items-center justify-center border transition ${
                    isCurrent 
                        ? 'bg-blue-700 text-white border-blue-800 ring-2 ring-blue-400' 
                        : isAnswered 
                            ? 'bg-emerald-100 text-emerald-800 border-emerald-300' 
                            : 'bg-slate-50 text-slate-600 border-slate-200 hover:bg-slate-100'
                }`;
                btn.innerText = i + 1;
                btn.onclick = () => {
                    state.quizState.currentQuestionIndex = i;
                    renderQuestion();
                };
                gridNav.appendChild(btn);
            }
        }

        function submitQuiz() {
            let correctCount = 0;
            currentQuestionsList.forEach((q, idx) => {
                if (state.quizState.userAnswers[idx] === q.correctIndex) {
                    correctCount++;
                }
            });

            const score = (correctCount / 20) * 100;
            const wrongCount = 20 - correctCount;

            document.getElementById('resultScore').innerText = score.toFixed(0);
            document.getElementById('resultCorrect').innerText = `${correctCount} / 20`;
            document.getElementById('resultWrong').innerText = `${wrongCount} / 20`;
            
            const statusBadge = document.getElementById('resultStatus');
            if (score >= 75) {
                statusBadge.innerText = 'TUNTAS (LULUS)';
                statusBadge.className = 'text-sm font-bold mt-1.5 text-emerald-600';
            } else {
                statusBadge.innerText = 'REMIDIAL';
                statusBadge.className = 'text-sm font-bold mt-1.5 text-rose-600';
            }

            // Render Explanations
            const expList = document.getElementById('explanationsList');
            expList.innerHTML = '';
            currentQuestionsList.forEach((q, idx) => {
                const isCorrect = state.quizState.userAnswers[idx] === q.correctIndex;
                const div = document.createElement('div');
                div.className = `p-3 rounded-xl border text-xs ${isCorrect ? 'bg-emerald-50/50 border-emerald-200' : 'bg-rose-50/50 border-rose-200'}`;
                div.innerHTML = `
                    <div class="font-bold text-slate-800">Soal ${idx + 1}: ${isCorrect ? '✓ Benar' : '✗ Salah'}</div>
                    <div class="text-slate-600 mt-1">${q.explanation}</div>
                `;
                expList.appendChild(div);
            });

            document.getElementById('quizContainer').classList.add('hidden');
            document.getElementById('quizResultPanel').classList.remove('hidden');
            lucide.createIcons();
        }

        function retryQuiz() {
            initQuiz();
        }

        // ==========================================
        // MODULE 3: INTERAKSI & AI CHAT LOGIC
        // ==========================================

        function handleChatSubmit(e) {
            e.preventDefault();
            const input = document.getElementById('chatInput');
            const message = input.value.trim();
            if (!message) return;

            const chatMessages = document.getElementById('chatMessages');

            // User Message
            const userMsgDiv = document.createElement('div');
            userMsgDiv.className = "flex gap-3 justify-end";
            userMsgDiv.innerHTML = `
                <div class="bg-blue-700 text-white p-3.5 rounded-2xl rounded-tr-none text-xs sm:text-sm max-w-[85%] shadow-xs">
                    ${message}
                </div>
            `;
            chatMessages.appendChild(userMsgDiv);
            input.value = '';
            chatMessages.scrollTop = chatMessages.scrollHeight;

            // Simulated AI Response
            setTimeout(() => {
                const aiMsgDiv = document.createElement('div');
                aiMsgDiv.className = "flex gap-3";
                aiMsgDiv.innerHTML = `
                    <div class="w-8 h-8 rounded-full bg-emerald-600 text-white flex items-center justify-center text-xs font-bold flex-shrink-0">AI</div>
                    <div class="bg-white p-3.5 rounded-2xl rounded-tl-none border border-slate-200 text-xs sm:text-sm text-slate-700 shadow-xs max-w-[85%]">
                        Terima kasih atas pertanyaannya mengenai <b>${state.currentSubject}</b>. Berdasarkan standar Kurikulum Nasional Scientists Learning Center, untuk menyelesaikan pertanyaan ini kita perlu memperhatikan dua langkah utama: 1) Identifikasi variabel utama, 2) Terapkan rumus standar. Apakah penjelasan ini cukup jelas?
                    </div>
                `;
                chatMessages.appendChild(aiMsgDiv);
                chatMessages.scrollTop = chatMessages.scrollHeight;
            }, 800);
        }

        function handleBookSession(e) {
            e.preventDefault();
            const tutor = document.getElementById('tutorSelect').value;
            alert(`[Scientists LC Booking]\nPermintaan sesi private tutor bersama "${tutor}" telah berhasil diajukan! Tim admin kami akan mengonfirmasi via WhatsApp.`);
        }

        // ==========================================
        // MODULE 4: MANAJEMEN & RAPOR LOGIC
        // ==========================================

        function renderAdminDashboard() {
            const container = document.getElementById('adminProgressBars');
            container.innerHTML = '';

            const subjects = LEVELS[state.currentLevel].subjects.slice(0, 6);

            subjects.forEach(subj => {
                const score = Math.floor(Math.random() * 20) + 80;
                const div = document.createElement('div');
                div.className = "space-y-1";
                div.innerHTML = `
                    <div class="flex justify-between text-xs font-semibold">
                        <span class="text-slate-700">${subj}</span>
                        <span class="text-emerald-600 font-bold">${score} / 100</span>
                    </div>
                    <div class="w-full bg-slate-100 rounded-full h-2.5 overflow-hidden">
                        <div class="bg-gradient-to-r from-blue-600 to-emerald-500 h-2.5 rounded-full" style="width: ${score}%"></div>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        function generateRapor() {
            alert(`[Scientists Learning Center - Rapor Akademik]\n\nNAMA SISWA: Ahmad Hidayat\nTINGKAT: ${state.currentLevel} (${state.currentClass})\nSEMESTER: ${state.currentSemester}\nRATA-RATA EVALUASI FORMATIF: 88.5 (Predikat A)\nSTATUS: LULUS SANGAT MEMUASKAN\n\nFile Rapor Bimbel Digital telah berhasil di-generate!`);
        }
    </script>
</body>
</html>
