# SCORM Generator for Moodle 🎓📦

Um gerador de pacotes SCORM 1.2 web-based e *serverless*. Transforma instantaneamente arquivos de vídeo (MP4) e legendas (SRT/VTT) em pacotes `.zip` prontos para serem importados no LMS Moodle. 

Todo o processamento de conversão e empacotamento é feito localmente no navegador do usuário, garantindo privacidade, segurança e velocidade (o arquivo de vídeo nunca faz upload para nenhum servidor).

## 🚀 Funcionalidades

- **Processamento 100% Local (Client-Side):** Utiliza a API do navegador e a biblioteca `JSZip` para ler os arquivos e gerar o pacote SCORM localmente.
- **Rastreamento de Conclusão Real (Anti-Fraude):** O player gerado contabiliza apenas o tempo de vídeo efetivamente assistido. Arrastar a barra de progresso para o final não dispara a conclusão da aula.
- **Retomada de Ponto (Bookmarking):** O player se comunica com a API SCORM do Moodle para salvar o momento exato em que o usuário parou, retomando automaticamente no próximo acesso.
- **Conversão Automática de Legendas:** Suporte nativo para `.vtt` e `.srt`. Arquivos SubRip (`.srt`) são convertidos dinamicamente em tempo de execução para WebVTT, o padrão suportado por players HTML5.
- **Legendas Dinâmicas e Responsivas:** Escala de fonte inteligente acompanhando a altura da tela (`clamp`), com tratamento seguro para quebras de linha e renderização de caixa de fundo contínua (evitando *gaps* entre blocos no Chrome/Edge).
- **Interface Intuitiva:** Suporte a Drag & Drop para adição rápida de arquivos.

## 🛠️ Tecnologias Utilizadas

- **HTML5 & CSS3:** Interface responsiva e design moderno (CSS variables).
- **JavaScript (Vanilla):** Lógica do player, cálculo de *watch time*, conversão SRT -> VTT e comunicação com a SCORM API (`cmi.core`).
- **[JSZip](https://stuk.github.io/jszip/):** Empacotamento do arquivo `.zip` sem depender de backend.

## ⚙️ Como Usar

1. Baixe ou clone este repositório.
2. Abra o arquivo `index.html` diretamente no seu navegador (não é necessário rodar um servidor local).
3. Selecione ou arraste o arquivo de vídeo (`.mp4`).
4. (Opcional) Selecione ou arraste o arquivo de legenda (`.srt` ou `.vtt`).
5. Defina o **Título da Aula** (este título aparecerá no player e na árvore do Moodle).
6. Defina a **Porcentagem Mínima** do vídeo que o aluno deve assistir de fato para que a nota `100` e o status `passed` sejam enviados ao Moodle.
7. Clique em **Gerar pacote SCORM (.zip)**.
8. Suba o arquivo gerado diretamente em uma atividade de "Pacote SCORM" no seu Moodle.

## 📝 Comunicação SCORM Implementada

O player gerado injeta um script (`scormInit()`) que rastreia e envia os seguintes parâmetros via SCORM 1.2:
- `cmi.core.lesson_status` (`passed`, `incomplete`)
- `cmi.core.score.raw` (0 a 100 baseando-se na % de cobertura assistida)
- `cmi.core.lesson_location` (tempo em segundos para retomada)
- `cmi.core.session_time` (tempo de sessão ativa)
- `cmi.core.exit` (`suspend`)

## 👨‍💻 Autor

Desenvolvido por **Natan Ayres**.
