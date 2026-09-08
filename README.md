# SCORM Generator for Moodle 🎓📦

[🇧🇷 Português](#-português) | [🇺🇸 English](#-english)

---

## 🇧🇷 Português

Um gerador de pacotes SCORM 1.2 web-based e *serverless*. Transforma instantaneamente arquivos de vídeo (MP4) e legendas (SRT/VTT) em pacotes `.zip` prontos para serem importados no LMS Moodle. 

Todo o processamento de conversão e empacotamento é feito localmente no navegador do usuário, garantindo privacidade, segurança e velocidade (o arquivo de vídeo nunca faz upload para nenhum servidor).

### 🚀 Funcionalidades
- **Processamento 100% Local (Client-Side):** Utiliza a API do navegador e a biblioteca `JSZip` para ler os arquivos e gerar o pacote SCORM localmente.
- **Rastreamento de Conclusão Real (Anti-Fraude):** O player gerado contabiliza apenas o tempo de vídeo efetivamente assistido. Arrastar a barra de progresso para o final não dispara a conclusão da aula.
- **Retomada de Ponto (Bookmarking):** O player se comunica com a API SCORM do Moodle para salvar o momento exato em que o usuário parou, retomando automaticamente no próximo acesso.
- **Conversão Automática de Legendas:** Suporte nativo para `.vtt` e `.srt`. Arquivos SubRip (`.srt`) são convertidos dinamicamente em tempo de execução para WebVTT, o padrão suportado por players HTML5.
- **Legendas Dinâmicas e Responsivas:** Escala de fonte inteligente acompanhando a altura da tela (`clamp`), com tratamento seguro para quebras de linha e renderização de caixa de fundo contínua (evitando *gaps* entre blocos no Chrome/Edge).
- **Interface Intuitiva:** Suporte a Drag & Drop para adição rápida de arquivos.

### 🛠️ Tecnologias Utilizadas
- **HTML5 & CSS3:** Interface responsiva e design moderno (CSS variables).
- **JavaScript (Vanilla):** Lógica do player, cálculo de *watch time*, conversão SRT -> VTT e comunicação com a SCORM API (`cmi.core`).
- **[JSZip](https://stuk.github.io/jszip/):** Empacotamento do arquivo `.zip` sem depender de backend.

### ⚙️ Como Usar
1. Baixe ou clone este repositório.
2. Abra o arquivo `index.html` diretamente no seu navegador (não é necessário rodar um servidor local).
3. Selecione ou arraste o arquivo de vídeo (`.mp4`).
4. (Opcional) Selecione ou arraste o arquivo de legenda (`.srt` ou `.vtt`).
5. Defina o **Título da Aula** (este título aparecerá no player e na árvore do Moodle).
6. Defina a **Porcentagem Mínima** do vídeo que o aluno deve assistir de fato para que a nota `100` e o status `passed` sejam enviados ao Moodle.
7. Clique em **Gerar pacote SCORM (.zip)**.
8. Suba o arquivo gerado diretamente em uma atividade de "Pacote SCORM" no seu Moodle.

### 📝 Comunicação SCORM Implementada
O player gerado injeta um script (`scormInit()`) que rastreia e envia os seguintes parâmetros via SCORM 1.2:
- `cmi.core.lesson_status` (`passed`, `incomplete`)
- `cmi.core.score.raw` (0 a 100 baseando-se na % de cobertura assistida)
- `cmi.core.lesson_location` (tempo em segundos para retomada)
- `cmi.core.session_time` (tempo de sessão ativa)
- `cmi.core.exit` (`suspend`)

---

## 🇺🇸 English

A web-based and serverless SCORM 1.2 package generator. It instantly transforms video files (MP4) and subtitles (SRT/VTT) into `.zip` packages ready to be imported into the Moodle LMS.

All processing, conversion, and packaging happens locally inside the user's browser, ensuring complete privacy, security, and speed (video files are never uploaded to any server).

### 🚀 Features
- **100% Local (Client-Side) Processing:** Uses browser APIs and the `JSZip` library to read files and generate SCORM packages locally.
- **Real Completion Tracking (Anti-Fraud):** The generated player tracks only the actual time spent watching the video. Dragging the progress bar to the end will not trigger lesson completion.
- **Bookmarking:** The player communicates with Moodle's SCORM API to save the exact timestamp where the user stopped, automatically resuming from that point on the next visit.
- **Automatic Subtitle Conversion:** Native support for `.vtt` and `.srt`. SubRip (`.srt`) files are dynamically converted at runtime to WebVTT, the standard format supported by HTML5 players.
- **Responsive Dynamic Subtitles:** Smart font scaling based on screen height (`clamp`), featuring clean multi-line handling and consistent background box rendering (avoiding gaps between blocks in Chrome/Edge).
- **Intuitive Interface:** Drag & Drop support for fast file adding.

### 🛠️ Built With
- **HTML5 & CSS3:** Responsive interface and modern design (CSS variables).
- **Vanilla JavaScript:** Player logic, watch-time calculation, SRT-to-VTT conversion, and communication with the SCORM API (`cmi.core`).
- **[JSZip](https://stuk.github.io/jszip/):** Backend-free `.zip` package generation.

### ⚙️ How to Use
1. Download or clone this repository.
2. Open the `index.html` file directly in your browser (no local server required).
3. Select or drag and drop your video file (`.mp4`).
4. (Optional) Select or drag and drop your subtitle file (`.srt` or `.vtt`).
5. Set the **Lesson Title** (this title will appear on the player and in the Moodle tree view).
6. Set the **Minimum Percentage** of the video the student must actually watch for a grade of `100` and a `passed` status to be sent to Moodle.
7. Click on **Gerar pacote SCORM (.zip)**.
8. Upload the generated `.zip` file directly into a "SCORM Package" activity in Moodle.

### 📝 Implemented SCORM Communication
The generated player injects a script (`scormInit()`) that tracks and sends the following parameters via SCORM 1.2:
- `cmi.core.lesson_status` (`passed`, `incomplete`)
- `cmi.core.score.raw` (0 to 100 based on watch coverage percentage)
- `cmi.core.lesson_location` (time in seconds for bookmarking)
- `cmi.core.session_time` (active session duration)
- `cmi.core.exit` (`suspend`)

---

## 👨‍💻 Author / Autor

Developed by **Natan Ayres**.
