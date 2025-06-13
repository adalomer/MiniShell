🐚 Minishell
Bir Unix kabuğunu sıfırdan yazmaya hazır mısın?
42 öğrencisinin yazdığı kendi küçük ama güçlü shell uygulaması

🎯 Proje Amacı
md
Kopyala
Düzenle
Minishell, bir Unix kabuğunun temel işlevlerini yeniden yazarak process, redirection,
signal, parsing, environment gibi temel sistem konularını öğretmeyi amaçlayan bir projedir.
📚 Özellikler
Özellikler	Açıklama
🖥️ Prompt	minishell$ gibi bir komut istemcisi
🧠 Parsing	Komutları doğru şekilde ayırma (quotes, pipes, redirections)
🚀 Execution	execve, fork, pipe, waitpid gibi sistem fonksiyonlarıyla komut çalıştırma
📦 Builtins	cd, echo, pwd, env, export, unset, exit gibi özel komutlar
🔀 Redirection	>, >>, <, << gibi giriş/çıkış yönlendirmeleri
🔗 Pipes	`
🌿 Environment Vars	$HOME, $PATH, $USER gibi değişkenleri yönetme
🛑 Signal Handling	Ctrl+C, Ctrl+\ gibi sinyalleri yönetme
💡 Exit Status	Her komut sonunda $? değeriyle çıkış kodu

🧩 Yapılandırma
cpp
Kopyala
Düzenle
minishell/
├── main.c                // Uygulama döngüsü
├── minishell.h           // Header dosyası
├── parser/               // Lexing & Parsing dosyaları
│   ├── lexer.c
│   └── parser.c
├── executor/             // Komutları çalıştırma
│   ├── executor.c
│   ├── pipe.c
│   └── redirection.c
├── builtins/             // Dahili komutlar
│   ├── cd.c
│   ├── export.c
│   └── ...
├── signals/              // Sinyal yönetimi
│   └── signals.c
├── env/                  // Environment değişkenleri
│   └── env_utils.c
├── utils/                // Yardımcı fonksiyonlar
│   ├── ft_split.c
│   └── string_utils.c
⚙️ Kullanılan Fonksiyonlar
📁 Kategori	🧠 Fonksiyonlar
Girdi / Çıktı	readline, dup2, open, close
Süreç Yönetimi	fork, execve, waitpid, pipe
Sinyal	signal, sigaction, kill
String	strtok, strjoin, getenv, ft_split

🔄 Uygulama Döngüsü
c
Kopyala
Düzenle
while (1)
{
	print_prompt();
	line = readline("minishell$ ");
	add_history(line);
	tokens = tokenize(line);
	commands = parse(tokens);
	execute(commands, envp);
	free_everything();
}
🧪 Test Örnekleri
bash
Kopyala
Düzenle
$ ls -la | grep minishell
$ echo "Hello" > out.txt && cat < out.txt
$ export NAME=Ömer && echo $NAME
$ cat << EOF
heredoc test
EOF
🌈 Bonus (isteğe bağlı)
&&, || gibi mantıksal operatörler

Komut gruplama: (ls && echo done)

*, ?.c gibi wildcard desteği

History dosyasına kayıt alma

jobs, fg, bg gibi job control özellikleri (zorunlu değil)

💥 Öğrendiklerim
✅ UNIX sistem çağrıları
✅ Shell tasarımı
✅ Process & Signal yönetimi
✅ Lexing ve parsing
✅ Bellek yönetimi (Valgrind 💚)

🧠 Kapanış Notu
Minishell projesi, düşük seviyeli programlamada uzmanlaşmak isteyen herkes için adeta bir sınavdır.

"Bir shell yazdın mı? Artık komut satırına başka gözle bakacaksın!"

🤝 Katkı ve Lisans
Bu proje 42 Network kapsamında gerçekleştirilmiştir.
Kodlar ve içerikler özgürce geliştirilebilir.
