Minishell
42 Projesi | Minimal bir Bash benzeri shell implementasyonu
Komut yorumlayıcısı, process yönetimi, piping, redirection, sinyaller ve ortam değişkenleri gibi temel UNIX kavramlarını öğrenmek için geliştirilmiştir.

🧠 Projenin Amacı
Minishell, bash veya zsh gibi temel bir kabuğun en temel fonksiyonlarını kendi ellerinle yeniden inşa etmeyi hedefler. Bu projeyle birlikte:

Shell ortamı tasarımı

Komut ayrıştırma (lexing/parsing)

Process oluşturma ve yönetme (fork / execve)

Pipe (|), yönlendirme (>, <, >>, <<)

Environment değişken yönetimi

Built-in komutlar

Sinyal yakalama ve yönetimi

Bellek yönetimi

gibi sistem programlamanın yapı taşlarını öğrenmiş olacaksın.

🧩 Proje Mimarisi
php
Kopyala
Düzenle
minishell/
├── main.c                   # Shell loop & readline
├── minishell.h              # Global yapılar & tanımlar
├── parser/                  # Tokenizer & command parser
│   ├── lexer.c
│   ├── parser.c
│   └── quotes.c
├── executor/                # Komut çalıştırma, fork, redir
│   ├── executor.c
│   ├── pipe.c
│   ├── redirection.c
├── builtins/                # Built-in komutlar
│   ├── cd.c, echo.c, exit.c, ...
├── env/                     # Env değişken yönetimi
│   └── env_utils.c
├── signals/                 # SIGINT, SIGQUIT handler
│   └── signals.c
├── utils/                   # Yardımcı fonksiyonlar
│   ├── ft_split.c, free_utils.c, ...
└── Makefile
⚙️ Çalışma Aşamaları
1. Readline & Input İşleme
readline() ile komut al

add_history() ile geçmişe ekle

Quotes (", '), pipe (|), redirection (<, >, <<, >>) ayrıştır

2. Parser
Tokenları command yapısına dönüştür

Argümanları ayır, heredoc varsa geçici dosyaya yaz

3. Executor
Komutu fork edip çalıştır

Gerekirse execve ile PATH içinde ara

Built-in ise doğrudan çalıştır (örn. cd, export, exit)

4. Redirection
dup2, open, close ile yönlendirme ayarları

> >>: stdout yönlendirme

<: input okuma

<<: heredoc, sınırlayıcıya kadar okuma

5. Pipes
pipe(), dup2() ve fork() ile çoklu komut zinciri

Örnek: ls | grep foo | wc -l

6. Environment Değişkenleri
export VAR=value, unset VAR, echo $VAR

$?, $PATH gibi değişkenlerin çözülmesi

Kendi ortam değişkeni linked list yapısı oluştur

7. Signals
SIGINT (Ctrl+C) → readline temizle, shell kapanmaz

SIGQUIT (Ctrl+\) → child’da çalışmalı

heredoc sırasında özel signal handler gerekebilir

8. Exit Status
Komut başarı durumuna göre $? güncellenir

command not found → 127, permission denied → 126

🛠️ Kullanılan Fonksiyonlar
Kategori	Fonksiyonlar
I/O & Exec	readline, write, open, close, dup2, execve, access, fork, pipe, waitpid
Signal	signal, sigaction, kill
Env	getenv, setenv (manuel), unsetenv
Parsing	strtok, strjoin, strdup, strchr, ft_split, malloc/free

🔧 Built-in Komutlar
Komut	Açıklama
cd	Dizini değiştir
echo	Argümanları yazdır
pwd	Geçerli dizini yazdır
exit	Shell’den çık
export	Env değişkeni ekle
unset	Env değişkenini sil
env	Tüm env değişkenlerini göster

✅ Test Edilmesi Gereken Örnekler
bash
Kopyala
Düzenle
ls -la | grep minishell
cat < infile | grep test > outfile
echo hello > file && cat file
export NAME=test && echo $NAME
cd ~/Desktop && pwd
echo $?
cat << EOF
heredoc test
EOF
🔥 Bonus (İsteğe Bağlı)
&&, || gibi mantıksal zincirler

(*.c) gibi wildcard desteği

(ls && echo ok) gibi komut grupları

Shell geçmişinin .history dosyasına yazılması

🔒 Kurallar
✅ Norminette uyumlu
✅ Bellek sızıntısı yok (Valgrind önerilir)
✅ Global değişken kullanımı yasak
✅ readline ve heredoc düzgün sinyal davranışı

🏁 Başlatmak İçin
bash
Kopyala
Düzenle
make
./minishell
📚 Öğrenilen Konular
Unix sistem çağrıları

Process yönetimi

File descriptor kavramı

Tokenizasyon & parser yazımı

Sinyal ve handler yönetimi

Memory leak avcılığı 🕵️

