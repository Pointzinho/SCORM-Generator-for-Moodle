# SCORM Generator for Moodle 🎓📦

[🇧🇷 Português](#-português) | [🇺🇸 English](#-english)

---

## 🇧🇷 Português

Um gerador de pacotes SCORM 1.2 web-based e *serverless*. Transforma instantaneamente arquivos de vídeo (MP4) e legendas (SRT/VTT) em pacotes `.zip` prontos para serem importados no LMS Moodle. 

Todo o processamento de conversão e empacotamento é feito localmente no navegador do usuário, garantindo privacidade, segurança e velocidade (o arquivo de vídeo nunca faz upload para nenhum servidor).

### 🚀 Funcionalidades
- **Processamento 100% Local (Client-Side):** Utiliza a API do navegador e a biblioteca `JSZip` para ler os arquivos e gerar o pacote SCORM localmente.
- **Rastreamento de Conclusão Real (Anti-Fraude):** O player gerado contabiliza a cobertura efetivamente reproduzida, organizada em 100 blocos MAP100. Arrastar a barra de progresso para o final não marca automaticamente os blocos intermediários nem dispara a conclusão da aula.
- **Rastreamento MAP100:** O vídeo é dividido logicamente em 100 blocos de cobertura. Cada bloco representa aproximadamente 1% do conteúdo e é marcado somente quando o trecho é reproduzido de forma válida.
- **Persistência da Cobertura:** O mapa MAP100 é salvo no Moodle por meio de `cmi.suspend_data`, permitindo que a porcentagem assistida continue de onde o aluno parou, mesmo depois de fechar e reabrir a atividade.
- **Proteção contra Saltos:** Saltos grandes na linha do tempo não são contabilizados automaticamente como conteúdo assistido. O player compara continuamente o avanço real do vídeo e ignora deltas anormais.
- **Validação do Pacote ZIP:** Antes do download, o gerador valida o pacote com o próprio JSZip e confirma a presença de `imsmanifest.xml`, `index.html` e `video.mp4`.
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
6. Defina a **Porcentagem Mínima** do vídeo que o aluno deve assistir de fato para que o status `passed` seja enviado ao Moodle. A nota `cmi.core.score.raw` representa a porcentagem real de cobertura assistida, de 0 a 100.
7. Clique em **Gerar pacote SCORM (.zip)**.
8. Suba o arquivo gerado diretamente em uma atividade de "Pacote SCORM" no seu Moodle.

### 📝 Comunicação SCORM Implementada
O player gerado injeta um script (`scormInit()`) que rastreia e envia os seguintes parâmetros via SCORM 1.2:
- `cmi.core.lesson_status` (`passed`, `incomplete`)
- `cmi.core.score.raw` (0 a 100, correspondente à cobertura MAP100 assistida)
- `cmi.core.score.min` (`0`)
- `cmi.core.score.max` (`100`)
- `cmi.core.lesson_location` (posição do vídeo em segundos para retomada)
- `cmi.suspend_data` (mapa MAP100 persistido para restaurar a cobertura acumulada)
- `cmi.core.session_time` (tempo da sessão ativa)
- `cmi.core.exit` (`suspend`)
> `cmi.core.lesson_location` e `cmi.suspend_data` têm funções diferentes. O primeiro salva o ponto de reprodução; o segundo salva o histórico compacto de cobertura assistida.
---

## 🇺🇸 English

A web-based and serverless SCORM 1.2 package generator. It instantly transforms video files (MP4) and subtitles (SRT/VTT) into `.zip` packages ready to be imported into the Moodle LMS.

All processing, conversion, and packaging happens locally inside the user's browser, ensuring complete privacy, security, and speed (video files are never uploaded to any server).

### 🚀 Features
- **100% Local (Client-Side) Processing:** Uses browser APIs and the `JSZip` library to read files and generate SCORM packages locally.
- **Real Completion Tracking (Anti-Fraud):** The generated player tracks effectively played coverage using 100 MAP100 blocks. Moving the progress bar to the end does not automatically mark intermediate blocks or complete the lesson.
- **MAP100 Tracking:** The video is logically divided into 100 coverage blocks. Each block represents approximately 1% of the content and is marked only when the corresponding segment is validly played.
- **Coverage Persistence:** The MAP100 coverage map is stored in Moodle through `cmi.suspend_data`, allowing the accumulated percentage to persist after the learner closes and reopens the activity.
- **Seek Protection:** Large timeline jumps are not automatically counted as watched content. The player continuously compares the actual playback delta and ignores abnormal jumps.
- **ZIP Validation:** Before downloading, the generator validates the package with JSZip and confirms the presence of `imsmanifest.xml`, `index.html`, and `video.mp4`.
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
6. Set the **Minimum Percentage** of the video the student must actually watch for the `passed` status to be sent to Moodle. The `cmi.core.score.raw` value represents the actual watched coverage percentage, from 0 to 100.
7. Click on **Gerar pacote SCORM (.zip)**.
8. Upload the generated `.zip` file directly into a "SCORM Package" activity in Moodle.

### 📝 Implemented SCORM Communication
The generated player injects a script (`scormInit()`) that tracks and sends the following parameters via SCORM 1.2:
- `cmi.core.lesson_status` (`passed`, `incomplete`)
- `cmi.core.score.raw` (0 to 100, corresponding to watched MAP100 coverage)
- `cmi.core.score.min` (`0`)
- `cmi.core.score.max` (`100`)
- `cmi.core.lesson_location` (video position in seconds for bookmarking)
- `cmi.suspend_data` (persisted MAP100 map used to restore accumulated coverage)
- `cmi.core.session_time` (active session duration)
- `cmi.core.exit` (`suspend`)
> `cmi.core.lesson_location` and `cmi.suspend_data` serve different purposes. The first stores the playback position; the second stores the compact history of watched coverage.

---

## 👨‍💻 Author / Autor

Developed by **Natan Ayres**.
