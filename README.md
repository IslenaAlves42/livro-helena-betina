<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Helena e Betina - Guardiãs do Reino das Fadas</title>
  <link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Quicksand:wght@500;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --primary: #ff6b9b;
      --secondary: #8a4fff;
      --accent: #ffd166;
      --bg: #2b1055;
      --panel-bg: #1c0a38;
    }

    * {
      box-sizing: border-box;
      user-select: none;
      -webkit-user-select: none;
    }

    body {
      margin: 0;
      padding: 0;
      background: var(--bg);
      font-family: 'Quicksand', sans-serif;
      color: white;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    header {
      width: 100%;
      background: rgba(0, 0, 0, 0.5);
      padding: 12px 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 4px 15px rgba(0,0,0,0.3);
      position: sticky;
      top: 0;
      z-index: 100;
      backdrop-filter: blur(8px);
    }

    h1 {
      font-family: 'Fredoka One', cursive;
      margin: 0;
      font-size: 1.4rem;
      color: #ff9ebb;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
    }

    .nav-tabs {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
    }

    .tab-btn {
      background: #4a2180;
      border: 2px solid #8a4fff;
      color: white;
      padding: 8px 16px;
      border-radius: 20px;
      font-family: 'Fredoka One', cursive;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    .tab-btn.active, .tab-btn:hover {
      background: var(--primary);
      border-color: #ff9ebb;
      transform: scale(1.05);
    }

    main {
      width: 100%;
      max-width: 1200px;
      padding: 20px;
      flex: 1;
    }

    .view-panel {
      display: none;
      width: 100%;
      flex-direction: column;
      align-items: center;
    }

    .view-panel.active {
      display: flex;
    }

    /* HQ GRID */
    .comic-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
      gap: 20px;
      width: 100%;
      padding: 10px 0;
    }

    .comic-card {
      background: var(--panel-bg);
      border: 3px solid var(--secondary);
      border-radius: 14px;
      overflow: hidden;
      cursor: pointer;
      transition: transform 0.25s ease, box-shadow 0.25s ease, border-color 0.25s ease;
      display: flex;
      flex-direction: column;
      box-shadow: 0 6px 15px rgba(0,0,0,0.4);
    }

    .comic-card:hover {
      transform: translateY(-6px) scale(1.02);
      border-color: var(--accent);
      box-shadow: 0 12px 25px rgba(255, 209, 102, 0.3);
    }

    .comic-card-img {
      width: 100%;
      height: 220px;
      object-fit: cover;
      background: #000;
      border-bottom: 2px solid var(--secondary);
    }

    .comic-card-body {
      padding: 12px;
      display: flex;
      flex-direction: column;
      gap: 6px;
      flex: 1;
    }

    .comic-card-tag {
      font-family: 'Fredoka One', cursive;
      font-size: 0.85rem;
      color: var(--accent);
    }

    .comic-card-text {
      font-size: 0.9rem;
      margin: 0;
      line-height: 1.3;
      color: #ddd;
      display: -webkit-box;
      -webkit-line-clamp: 4;
      -webkit-box-orient: vertical;
      overflow: hidden;
    }

    /* MODAL HQ */
    .modal-overlay {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background: rgba(10, 3, 25, 0.92);
      z-index: 1000;
      justify-content: center;
      align-items: center;
      padding: 20px;
      backdrop-filter: blur(5px);
    }

    .modal-overlay.active {
      display: flex;
    }

    .modal-content {
      background: var(--panel-bg);
      border: 4px solid var(--accent);
      border-radius: 16px;
      max-width: 900px;
      width: 100%;
      max-height: 90vh;
      display: flex;
      flex-direction: column;
      overflow: hidden;
      position: relative;
      box-shadow: 0 20px 50px rgba(0,0,0,0.8);
    }

    .modal-close {
      position: absolute;
      top: 10px;
      right: 15px;
      background: var(--primary);
      border: 2px solid #fff;
      color: white;
      font-family: 'Fredoka One', cursive;
      font-size: 1.2rem;
      border-radius: 50%;
      width: 36px;
      height: 36px;
      cursor: pointer;
      z-index: 10;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .modal-body {
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 15px;
      overflow-y: auto;
    }

    .modal-img {
      max-width: 100%;
      max-height: 55vh;
      object-fit: contain;
      border-radius: 8px;
      border: 2px solid var(--secondary);
    }

    .modal-text {
      font-size: 1.1rem;
      text-align: left;
      margin: 15px 0 0 0;
      line-height: 1.6;
      color: #fff;
      white-space: pre-line;
      width: 100%;
      padding: 0 10px;
    }

    .modal-controls {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 12px 20px;
      background: rgba(0,0,0,0.4);
      border-top: 2px solid var(--secondary);
      gap: 10px;
    }

    /* PINTURA */
    .paint-workspace {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 15px;
      width: 100%;
    }

    .canvas-wrapper {
      position: relative;
      border: 4px solid #ffd166;
      border-radius: 12px;
      overflow: hidden;
      box-shadow: 0 8px 25px rgba(0,0,0,0.6);
      background: white;
      max-width: 800px;
      width: 100%;
      aspect-ratio: 4/3;
      cursor: crosshair;
      touch-action: none;
    }

    canvas#paintCanvas {
      width: 100%;
      height: 100%;
      display: block;
    }

    .toolbar {
      background: var(--panel-bg);
      border: 2px solid var(--secondary);
      border-radius: 15px;
      padding: 15px 20px;
      display: flex;
      flex-direction: column;
      gap: 12px;
      justify-content: center;
      align-items: center;
      width: 100%;
      max-width: 800px;
    }

    .tool-row {
      display: flex;
      flex-wrap: wrap;
      gap: 12px;
      justify-content: center;
      align-items: center;
      width: 100%;
    }

    .tool-group {
      display: flex;
      align-items: center;
      gap: 8px;
      background: rgba(0,0,0,0.25);
      padding: 6px 12px;
      border-radius: 20px;
      border: 1px solid rgba(255,255,255,0.1);
    }

    .tool-btn {
      background: #4a2180;
      border: 2px solid #8a4fff;
      color: white;
      padding: 6px 14px;
      border-radius: 15px;
      font-family: 'Fredoka One', cursive;
      font-size: 0.9rem;
      cursor: pointer;
      transition: all 0.2s;
    }

    .tool-btn.active, .tool-btn:hover {
      background: var(--primary);
      border-color: var(--accent);
      transform: scale(1.05);
    }

    .size-btn {
      width: 32px;
      height: 32px;
      border-radius: 50%;
      background: #4a2180;
      border: 2px solid #8a4fff;
      color: white;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      transition: all 0.2s;
    }

    .size-btn.active {
      background: var(--primary);
      border-color: var(--accent);
      transform: scale(1.15);
      box-shadow: 0 0 8px var(--accent);
    }

    .size-dot {
      background: white;
      border-radius: 50%;
    }

    .palette {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
      justify-content: center;
    }

    .color-swatch {
      width: 34px;
      height: 34px;
      border-radius: 50%;
      border: 2px solid white;
      cursor: pointer;
      transition: transform 0.2s;
    }

    .color-swatch.selected {
      transform: scale(1.25);
      border-color: #ffd166;
      box-shadow: 0 0 10px #ffd166;
    }

    .page-selector {
      display: flex;
      gap: 8px;
      overflow-x: auto;
      padding: 10px 5px;
      width: 100%;
      max-width: 800px;
      background: rgba(0,0,0,0.2);
      border-radius: 10px;
    }

    .page-thumb-box {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-width: 70px;
      height: 65px;
      border-radius: 8px;
      border: 2px solid var(--secondary);
      cursor: pointer;
      background: #31125e;
      font-family: 'Fredoka One', cursive;
      font-size: 0.8rem;
      color: #ffd166;
      transition: all 0.2s;
    }

    .page-thumb-box.active {
      border-color: #ffd166;
      background: var(--primary);
      color: white;
      transform: scale(1.08);
      box-shadow: 0 0 8px #ffd166;
    }

    .btn {
      background: var(--primary);
      border: none;
      color: white;
      padding: 8px 18px;
      border-radius: 25px;
      font-family: 'Fredoka One', cursive;
      font-size: 0.95rem;
      cursor: pointer;
      box-shadow: 0 4px 10px rgba(0,0,0,0.3);
      transition: all 0.2s;
    }

    .btn:hover {
      transform: translateY(-2px);
      background: #ff528a;
    }

    .btn:disabled {
      opacity: 0.4;
      cursor: not-allowed;
      transform: none;
    }

    .audio-btn {
      background: #8a4fff;
      border: 2px solid #ffd166;
    }

    /* JOGO */
    .game-container {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 15px;
      width: 100%;
      max-width: 800px;
    }

    .game-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      width: 100%;
      background: var(--panel-bg);
      border: 2px solid var(--secondary);
      border-radius: 12px;
      padding: 10px 20px;
      font-family: 'Fredoka One', cursive;
      font-size: 1.1rem;
      flex-wrap: wrap;
      gap: 10px;
    }

    .game-canvas-box {
      position: relative;
      width: 100%;
      aspect-ratio: 4/3;
      border: 4px solid var(--accent);
      border-radius: 14px;
      overflow: hidden;
      box-shadow: 0 8px 25px rgba(0,0,0,0.6);
      background: #190938;
      touch-action: none;
    }

    #gameCanvas {
      width: 100%;
      height: 100%;
      display: block;
    }

    .char-picker {
      display: flex;
      gap: 10px;
      align-items: center;
      justify-content: center;
      background: var(--panel-bg);
      padding: 10px 20px;
      border-radius: 12px;
      border: 2px solid var(--secondary);
      flex-wrap: wrap;
    }

    .char-btn {
      background: #4a2180;
      border: 2px solid #8a4fff;
      color: white;
      padding: 8px 14px;
      border-radius: 15px;
      font-family: 'Fredoka One', cursive;
      cursor: pointer;
      transition: all 0.2s;
    }

    .char-btn.selected {
      background: var(--primary);
      border-color: var(--accent);
      transform: scale(1.08);
      box-shadow: 0 0 10px var(--accent);
    }
  </style>
</head>
<body>

  <header>
    <h1>✨ Helena & Betina</h1>
    <div class="nav-tabs">
      <button class="tab-btn active" onclick="switchTab('reader')">📖 História em HQ</button>
      <button class="tab-btn" onclick="switchTab('painter')">🎨 Colorir</button>
      <button class="tab-btn" onclick="switchTab('game')">⭐ Jogar</button>
    </div>
  </header>

  <main>
    <section id="readerView" class="view-panel active">
      <div class="comic-grid" id="comicGrid"></div>
    </section>

    <section id="painterView" class="view-panel">
      <div class="paint-workspace">
        <div class="page-selector" id="thumbList"></div>

        <div class="canvas-wrapper" id="canvasBox">
          <canvas id="paintCanvas"></canvas>
        </div>

        <div class="toolbar">
          <div class="tool-row">
            <div class="tool-group">
              <span style="font-family: 'Fredoka One'; font-size: 0.85rem;">Modo:</span>
              <button class="tool-btn active" id="btnModeBucket" onclick="setPaintMode('bucket')">🪣 Balde</button>
              <button class="tool-btn" id="btnModeBrush" onclick="setPaintMode('brush')">🖌️ Pincel</button>
            </div>

            <div class="tool-group" id="brushSizeGroup">
              <span style="font-family: 'Fredoka One'; font-size: 0.85rem;">Pincel:</span>
              <button class="size-btn" onclick="setBrushSize(5)" id="size5"><div class="size-dot" style="width: 5px; height: 5px;"></div></button>
              <button class="size-btn active" onclick="setBrushSize(15)" id="size15"><div class="size-dot" style="width: 10px; height: 10px;"></div></button>
              <button class="size-btn" onclick="setBrushSize(30)" id="size30"><div class="size-dot" style="width: 16px; height: 16px;"></div></button>
              <button class="size-btn" onclick="setBrushSize(50)" id="size50"><div class="size-dot" style="width: 22px; height: 22px;"></div></button>
            </div>

            <button class="btn" onclick="clearCanvas()">🗑️ Limpar</button>
            <button class="btn" onclick="downloadArt()">💾 Salvar</button>
          </div>

          <div class="palette" id="colorPalette"></div>
        </div>
      </div>
    </section>

    <section id="gameView" class="view-panel">
      <div class="game-container">
        <div class="char-picker">
          <span style="font-family: 'Fredoka One';">Escolha seu Herói:</span>
          <button class="char-btn selected" id="btnHelena" onclick="selectGameChar('helena')">👩🏼 Helena</button>
          <button class="char-btn" id="btnBetina" onclick="selectGameChar('betina')">👧🏻 Betina</button>
          <button class="char-btn" id="btnUnicornio" onclick="selectGameChar('unicornio')">🦄 Unicórnio</button>
          <button class="char-btn" id="btnLumix" onclick="selectGameChar('lumix')">🪲 Lumix</button>
        </div>

        <div class="game-header">
          <span>⭐ Pontos: <span id="gameScore" style="color: var(--accent);">0</span></span>
          <span>❤️ Vidas: <span id="gameLives" style="color: #ff4757;">❤️❤️❤️</span></span>
          <button class="btn" id="btnStartGame" onclick="startGame()">▶️ Iniciar Jogo</button>
        </div>

        <div class="game-canvas-box">
          <canvas id="gameCanvas"></canvas>
        </div>
      </div>
    </section>
  </main>

  <div class="modal-overlay" id="imageModal">
    <div class="modal-content">
      <button class="modal-close" onclick="closeModal()">✕</button>
      <div class="modal-body">
        <img id="modalImg" class="modal-img" src="" alt="Página Completa">
        <p id="modalText" class="modal-text"></p>
      </div>
      <div class="modal-controls">
        <button class="btn" id="modalPrevBtn" onclick="navigateModal(-1)">◄ Anterior</button>
        <button class="btn audio-btn" id="speechToggleBtn" onclick="toggleAudio()">🔊 Ouvir</button>
        <span id="modalPageTag" style="font-family: 'Fredoka One'; font-size: 1.1rem; color: #ffd166;"></span>
        <button class="btn" id="modalNextBtn" onclick="navigateModal(1)">Próximo ►</button>
      </div>
    </div>
  </div>

  <script>
    const storyData = [
      { id: 'capa', title: 'Capa', img: 'capa.png', text: 'Helena e Betina: As Guardiãs do Reino das Fadas. Uma aventura cheia de magia, amizade e cores!' },
      { id: 1, title: 'Página 1', img: 'pagina1.png', text: 'Em um lugar escondido entre as nuvens, onde as flores brilhavam como estrelas e os riachos cantavam doces melodias, existia o Reino das Fadas. Ali moravam duas irmãs muito especiais: Helena e Betina. Helena tinha lindos cabelos longos e soltos. Betina tinha cabelos curtinhos e um sorriso que iluminava qualquer lugar. Juntas, elas protegiam toda a magia do reino.' },
      { id: 2, title: 'Página 2', img: 'pagina2.png', text: 'Todas as manhãs, as duas voavam pelos jardins encantados, cumprimentando as borboletas coloridas, os coelhos mágicos e os passarinhos dourados. Cada flor florescia ainda mais quando elas passavam espalhando um delicado pó de fada.' },
      { id: 3, title: 'Página 3', img: 'pagina3.png', text: 'Naquele dia, porém, algo estava diferente. As flores pareciam tristes, os riachos haviam parado de cantar e até o arco-íris estava perdendo suas cores. Helena olhou para Betina e disse:\n— Acho que o Reino das Fadas precisa da nossa ajuda.' },
      { id: 4, title: 'Página 4', img: 'pagina4.png', text: 'As duas correram até o Castelo de Cristal, onde a Rainha Luminara as esperava. A rainha explicou que a Estrela da Harmonia, responsável por espalhar alegria por todo o reino, havia desaparecido durante a noite.' },
      { id: 5, title: 'Página 5', img: 'pagina5.png', text: '— Apenas duas fadas de coração puro poderão encontrá-la — disse a rainha.\nHelena e Betina aceitaram a missão sem pensar duas vezes. Pegaram suas pequenas mochilas mágicas e partiram em uma grande aventura.' },
      { id: 6, title: 'Página 6', img: 'pagina6.png', text: 'A primeira parada foi a Floresta dos Sussurros. As árvores conversavam baixinho e indicavam o caminho apenas para quem soubesse ouvir com atenção. As irmãs fecharam os olhos e escutaram o vento.' },
      { id: 7, title: 'Página 7', img: 'pagina7.png', text: 'Seguindo a voz das árvores, elas encontraram um pequeno unicórnio preso entre galhos espinhosos. Sem demora, libertaram o filhote, que agradeceu com um brilho em seu chifre.' },
      { id: 8, title: 'Página 8', img: 'pagina8.png', text: 'Como recompensa, o unicórnio entregou uma pena prateada. Esta pena sempre apontará para a verdadeira esperança quando vocês estiverem perdidas.' },
      { id: 9, title: 'Página 9', img: 'pagina9.png', text: 'A pena começou a brilhar e conduziu as irmãs até uma enorme ponte de arco-íris. Mas a ponte estava quebrada, e um grande espaço vazio impedia a passagem.' },
      { id: 10, title: 'Página 10', img: 'pagina10.png', text: 'Helena teve uma ideia. As duas uniram seus poderes e espalharam pó mágico sobre a ponte. Pouco a pouco, as cores voltaram e o arco-íris ficou inteiro novamente.' },
      { id: 11, title: 'Página 11', img: 'pagina11.png', text: 'Depois da ponte havia um lago tão calmo que parecia um espelho. Quando olharam para a água, não viram seus rostos, mas sim seus maiores sonhos.' },
      { id: 12, title: 'Página 12', img: 'pagina12.png', text: 'Helena sonhava em proteger todas as crianças do Reino das Fadas. Betina sonhava em fazer qualquer criatura triste voltar a sorrir. O lago brilhou intensamente ao ouvir aqueles desejos tão bondosos.' },
      { id: 13, title: 'Página 13', img: 'pagina13.png', text: 'De repente, surgiu Lumix, um pequeno vaga-lume dourado.\n— Estou procurando vocês! Sei onde a Estrela da Harmonia esteve pela última vez.' },
      { id: 14, title: 'Página 14', img: 'pagina14.png', text: 'Lumix conduziu as irmãs até a Montanha da Luz. Lá encontraram pegadas escuras que nunca haviam visto antes. Alguém misterioso havia passado por ali.' },
      { id: 15, title: 'Página 15', img: 'pagina15.png', text: 'No alto da montanha apareceu a Sombra Cinzenta, envolvida por uma névoa escura.\n— A alegria do reino acabará para sempre! — gritou ela.' },
      { id: 16, title: 'Página 16', img: 'pagina16.png', text: 'Helena e Betina não sentiram medo. Elas deram as mãos e lembraram de todas as pessoas e criaturas que amavam. Uma luz dourada começou a surgir entre elas.' },
      { id: 17, title: 'Página 17', img: 'pagina17.png', text: 'A Sombra tentou apagar aquela luz, mas quanto mais amizade e amor as irmãs demonstravam, mais forte ela ficava.' },
      { id: 18, title: 'Página 18', img: 'pagina18.png', text: 'Sem conseguir vencer, a Sombra revelou um grande segredo:\n— Eu não nasci má... Apenas fiquei sozinha por muito tempo.' },
      { id: 19, title: 'Página 19', img: 'pagina19.png', text: 'Helena sorriu e respondeu:\n— Ninguém precisa ficar sozinho.\nBetina estendeu a mão para a Sombra.' },
      { id: 20, title: 'Página 20', img: 'pagina20.png', text: 'Naquele instante, toda a escuridão desapareceu. Em seu lugar surgiu uma pequena fada chamada Neblina, que havia perdido sua luz muitos anos antes.' },
      { id: 21, title: 'Página 21', img: 'pagina21.png', text: 'Neblina devolveu a Estrela da Harmonia às duas irmãs.\n— Obrigada por acreditarem em mim quando ninguém mais acreditava.' },
      { id: 22, title: 'Página 22', img: 'pagina22.png', text: 'Assim que a estrela voltou ao céu, todas as flores floresceram novamente. Os rios cantaram, os pássaros dançaram e o arco-íris brilhou mais forte do que nunca.' },
      { id: 23, title: 'Página 23', img: 'pagina23.png', text: 'Os animais mágicos organizaram uma linda festa. Coelhos, esquilos, unicórnios, dragõezinhos e borboletas celebravam a coragem das duas irmãs.' },
      { id: 24, title: 'Página 24', img: 'pagina24.png', text: 'A Rainha Luminara colocou uma linda medalha dourada em cada uma delas.\n— Vocês provaram que o maior poder de uma fada é a bondade.' },
      { id: 25, title: 'Página 25', img: 'pagina25.png', text: 'Naquela noite, Helena e Betina voaram bem alto e observaram milhares de estrelas iluminando o Reino das Fadas.' },
      { id: 26, title: 'Página 26', img: 'pagina26.png', text: 'Enquanto admiravam o céu, uma estrela cadente deixou cair uma pequena chave de cristal bem diante delas.' },
      { id: 27, title: 'Página 27', img: 'pagina27.png', text: 'A chave possuía um símbolo desconhecido que nenhuma fada jamais tinha visto. Lumix ficou curioso e disse:\n— Acho que essa chave abre um lugar secreto.' },
      { id: 28, title: 'Página 28', img: 'pagina28.png', text: 'Ao longe, uma enorme porta dourada surgiu entre as nuvens. Ela estava fechada havia centenas de anos e agora começava a brilhar lentamente.' },
      { id: 29, title: 'Página 29', img: 'pagina29.png', text: 'Helena segurou a chave e sorriu para Betina.\n— Parece que nossa próxima aventura está apenas começando.' },
      { id: 30, title: 'Página 30', img: 'pagina30.png', text: 'As duas deram as mãos, abriram suas asas e voaram em direção ao horizonte, prontas para descobrir novos mistérios, ajudar novos amigos e proteger para sempre toda a magia do Reino das Fadas.' },
      { 
        id: 31, 
        title: 'Página 31', 
        img: 'pagina31.png', 
        text: `Para minha querida Helena

Minha princesa Helena,
Este livro foi escrito especialmente para você.

Sempre que abrir estas páginas, lembre-se de que existe um lugar mágico onde tudo é possível: o mundo da imaginação. É nele que os sonhos ganham asas, a coragem vence o medo, a bondade transforma corações e as aventuras nunca têm fim.

Assim como a fada Helena desta história, desejo que você cresça acreditando na força do amor, da amizade, da esperança e da gentileza. Que nunca deixe de sonhar, de fazer perguntas, de descobrir coisas novas e de enxergar a beleza nas pequenas maravilhas da vida.

Cada página deste livro guarda um pedacinho do carinho que sinto por você. Espero que, sempre que o ler, seu coração se encha de alegria e sua imaginação voe tão alto quanto as asas das fadas.

Nunca deixe que ninguém diga que sonhar é bobagem. São os sonhos que inspiram grandes discoveries, criam histórias inesquecíveis e tornam o mundo um lugar mais bonito.

Que você tenha a coragem de enfrentar os desafios, a sabedoria para aprender com cada aventura e um coração cheio de amor para espalhar luz por onde passar.

E lembre-se de uma coisa muito importante: a verdadeira magia não está nas varinhas, nas asas ou no pó de fada. Ela mora dentro de você. Está no seu sorriso, na sua bondade, na sua criatividade e na capacidade de fazer o bem às pessoas.

Enquanto existir uma criança capaz de imaginar, o Reino das Fadas continuará vivo. E tenho certeza de que você sempre será uma de suas mais especiais guardiãs.

Com todo o meu amor,
Da titia Islena, que sempre acreditará na sua magia. ✨🧚🏻💕` 
      },
      { id: 'contracapa', title: 'Contracapa', img: 'contracapa.png', text: 'Fim! Esperamos que se tenha divertido a ler e a colorir esta história mágica.' }
    ];

    let currentModalIndex = 0;
    let selectedFemaleVoice = null;

    function loadVoices() {
      const voices = window.speechSynthesis.getVoices();
      selectedFemaleVoice = voices.find(v => v.lang.startsWith('pt') && (
        v.name.includes('Luciana') || 
        v.name.includes('Maria') || 
        v.name.includes('Francisca') || 
        v.name.includes('Vitória') ||
        v.name.includes('Female') ||
        v.name.includes('Google português')
      )) || voices.find(v => v.lang.startsWith('pt'));
    }

    if ('speechSynthesis' in window) {
      window.speechSynthesis.onvoiceschanged = loadVoices;
      loadVoices();
    }

    function speakCurrentPage() {
      if (!('speechSynthesis' in window)) return;
      window.speechSynthesis.cancel();

      const text = storyData[currentModalIndex].text;
      const utterance = new SpeechSynthesisUtterance(text);
      
      if (selectedFemaleVoice) utterance.voice = selectedFemaleVoice;
      utterance.lang = 'pt-BR';
      utterance.rate = 0.88; 
      utterance.pitch = 1.15; 

      document.getElementById('speechToggleBtn').innerText = '⏸️ Pausar';
      utterance.onend = () => {
        document.getElementById('speechToggleBtn').innerText = '🔊 Ouvir';
      };

      window.speechSynthesis.speak(utterance);
    }

    function toggleAudio() {
      if (window.speechSynthesis.speaking) {
        window.speechSynthesis.cancel();
        document.getElementById('speechToggleBtn').innerText = '🔊 Ouvir';
      } else {
        speakCurrentPage();
      }
    }

    function renderComicGrid() {
      const grid = document.getElementById('comicGrid');
      grid.innerHTML = '';

      storyData.forEach((item, index) => {
        const card = document.createElement('div');
        card.className = 'comic-card';
        card.onclick = () => openModal(index);

        card.innerHTML = `
          <img class="comic-card-img" src="${item.img}" alt="${item.title}" loading="lazy" onerror="this.onerror=null; this.parentElement.style.background='#1c0a38';">
          <div class="comic-card-body">
            <span class="comic-card-tag">${item.title}</span>
            <p class="comic-card-text">${item.text}</p>
          </div>
        `;
        grid.appendChild(card);
      });
    }

    function openModal(index) {
      currentModalIndex = index;
      updateModalContent();
      document.getElementById('imageModal').classList.add('active');
      speakCurrentPage();
    }

    function closeModal() {
      window.speechSynthesis.cancel();
      document.getElementById('imageModal').classList.remove('active');
    }

    function updateModalContent() {
      const page = storyData[currentModalIndex];
      document.getElementById('modalImg').src = page.img;
      document.getElementById('modalText').innerText = page.text;
      document.getElementById('modalPageTag').innerText = page.title;

      document.getElementById('modalPrevBtn').disabled = currentModalIndex === 0;
      document.getElementById('modalNextBtn').disabled = currentModalIndex === storyData.length - 1;
    }

    function navigateModal(delta) {
      const newIndex = currentModalIndex + delta;
      if (newIndex >= 0 && newIndex < storyData.length) {
        currentModalIndex = newIndex;
        updateModalContent();
        speakCurrentPage();
      }
    }

    document.getElementById('imageModal').addEventListener('click', (e) => {
      if (e.target.id === 'imageModal') closeModal();
    });

    function switchTab(tab) {
      window.speechSynthesis.cancel();
      document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
      document.querySelectorAll('.view-panel').forEach(p => p.classList.remove('active'));

      if (tab === 'reader') {
        document.querySelectorAll('.tab-btn')[0].classList.add('active');
        document.getElementById('readerView').classList.add('active');
      } else if (tab === 'painter') {
        document.querySelectorAll('.tab-btn')[1].classList.add('active');
        document.getElementById('painterView').classList.add('active');
        initPainter();
      } else if (tab === 'game') {
        document.querySelectorAll('.tab-btn')[2].classList.add('active');
        document.getElementById('gameView').classList.add('active');
        initGame();
      }
    }

    /* PINTURA */
    const canvas = document.getElementById('paintCanvas');
    const ctx = canvas.getContext('2d', { willReadFrequently: true });
    
    let activePaintIndex = 0;
    let baseImage = new Image();
    
    let currentHexColor = '#ff6b9b';
    let currentColorRgb = [255, 107, 155];
    let currentMode = 'bucket'; 
    let currentBrushSize = 15;
    let isDrawing = false;

    const colorsList = [
      '#ff4757', '#ff6b81', '#ffa502', '#eccc68',
      '#2ed573', '#1e90ff', '#70a1ff', '#a29bfe',
      '#e84393', '#ffffff', '#2f3542'
    ];

    function hexToRgb(hex) {
      const bigint = parseInt(hex.replace('#', ''), 16);
      return [(bigint >> 16) & 255, (bigint >> 8) & 255, bigint & 255];
    }

    function setPaintMode(mode) {
      currentMode = mode;
      document.getElementById('btnModeBucket').classList.toggle('active', mode === 'bucket');
      document.getElementById('btnModeBrush').classList.toggle('active', mode === 'brush');
    }

    function setBrushSize(size) {
      currentBrushSize = size;
      document.querySelectorAll('.size-btn').forEach(btn => btn.classList.remove('active'));
      document.getElementById('size' + size).classList.add('active');
    }

    function initPainter() {
      const thumbList = document.getElementById('thumbList');
      if (thumbList.children.length === 0) {
        storyData.forEach((item, idx) => {
          const box = document.createElement('div');
          box.className = 'page-thumb-box' + (idx === 0 ? ' active' : '');
          box.innerText = item.title;
          box.onclick = () => loadColorPage(idx, box);
          thumbList.appendChild(box);
        });

        const palette = document.getElementById('colorPalette');
        colorsList.forEach((col, idx) => {
          const swatch = document.createElement('div');
          swatch.className = 'color-swatch' + (idx === 0 ? ' selected' : '');
          swatch.style.background = col;
          swatch.onclick = () => {
            document.querySelectorAll('.color-swatch').forEach(s => s.classList.remove('selected'));
            swatch.classList.add('selected');
            currentHexColor = col;
            currentColorRgb = hexToRgb(col);
          };
          palette.appendChild(swatch);
        });

        canvas.addEventListener('pointerdown', handlePointerDown);
        canvas.addEventListener('pointermove', handlePointerMove);
        window.addEventListener('pointerup', handlePointerUp);

        loadColorPage(0);
      }
    }

    function getCanvasCoords(e) {
      const rect = canvas.getBoundingClientRect();
      const scaleX = canvas.width / rect.width;
      const scaleY = canvas.height / rect.height;
      return {
        x: Math.floor((e.clientX - rect.left) * scaleX),
        y: Math.floor((e.clientY - rect.top) * scaleY)
      };
    }

    function handlePointerDown(e) {
      const pos = getCanvasCoords(e);

      if (currentMode === 'bucket') {
        floodFill(pos.x, pos.y, currentColorRgb);
      } else {
        isDrawing = true;
        ctx.beginPath();
        ctx.moveTo(pos.x, pos.y);
        ctx.lineCap = 'round';
        ctx.lineJoin = 'round';
        ctx.strokeStyle = currentHexColor;
        ctx.lineWidth = currentBrushSize;
        ctx.lineTo(pos.x, pos.y);
        ctx.stroke();
      }
    }

    function handlePointerMove(e) {
      if (!isDrawing || currentMode !== 'brush') return;
      const pos = getCanvasCoords(e);
      ctx.lineTo(pos.x, pos.y);
      ctx.stroke();
    }

    function handlePointerUp() {
      if (isDrawing) {
        isDrawing = false;
        ctx.closePath();
      }
    }

    function generateFallbackDrawing(title) {
      canvas.width = 800;
      canvas.height = 600;
      ctx.fillStyle = '#ffffff';
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      ctx.strokeStyle = '#2f3542';
      ctx.lineWidth = 6;
      ctx.lineCap = 'round';

      ctx.beginPath();
      ctx.arc(400, 200, 70, 0, Math.PI * 2); 
      ctx.stroke();

      ctx.beginPath();
      ctx.arc(375, 185, 8, 0, Math.PI * 2);
      ctx.arc(425, 185, 8, 0, Math.PI * 2);
      ctx.fillStyle = '#2f3542';
      ctx.fill();

      ctx.beginPath();
      ctx.arc(400, 215, 25, 0.2, Math.PI - 0.2);
      ctx.stroke();

      ctx.beginPath();
      ctx.ellipse(300, 260, 60, 110, -Math.PI / 6, 0, Math.PI * 2);
      ctx.ellipse(500, 260, 60, 110, Math.PI / 6, 0, Math.PI * 2);
      ctx.stroke();

      ctx.beginPath();
      ctx.moveTo(370, 270);
      ctx.lineTo(430, 270);
      ctx.lineTo(450, 480);
      ctx.lineTo(350, 480);
      ctx.closePath();
      ctx.stroke();

      ctx.beginPath();
      ctx.arc(160, 450, 35, 0, Math.PI * 2);
      ctx.arc(640, 450, 35, 0, Math.PI * 2);
      ctx.stroke();

      ctx.fillStyle = '#2b1055';
      ctx.font = 'bold 24px Quicksand';
      ctx.textAlign = 'center';
      ctx.fillText(`🎨 Desenho de Colorir: ${title}`, 400, 560);
    }

    function loadColorPage(index, thumbEl) {
      activePaintIndex = index;
      if (thumbEl) {
        document.querySelectorAll('.page-thumb-box').forEach(t => t.classList.remove('active'));
        thumbEl.classList.add('active');
      }

      baseImage = new Image();
      baseImage.src = storyData[index].img;

      baseImage.onload = () => {
        canvas.width = baseImage.naturalWidth || 800;
        canvas.height = baseImage.naturalHeight || 600;
        clearCanvas();
      };

      baseImage.onerror = () => {
        generateFallbackDrawing(storyData[index].title);
      };
    }

    function clearCanvas() {
      if (baseImage.complete && baseImage.naturalWidth !== 0) {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        ctx.drawImage(baseImage, 0, 0, canvas.width, canvas.height);
      } else {
        generateFallbackDrawing(storyData[activePaintIndex].title);
      }
    }

    function floodFill(startX, startY, fillColor) {
      const imgData = ctx.getImageData(0, 0, canvas.width, canvas.height);
      const data = imgData.data;

      const width = canvas.width;
      const height = canvas.height;
      const startPos = (startY * width + startX) * 4;

      const startR = data[startPos];
      const startG = data[startPos + 1];
      const startB = data[startPos + 2];

      if (
        (startR === fillColor[0] && startG === fillColor[1] && startB === fillColor[2]) ||
        (startR < 50 && startG < 50 && startB < 50)
      ) {
        return;
      }

      function colorMatch(pos) {
        const r = data[pos];
        const g = data[pos + 1];
        const b = data[pos + 2];

        if (r < 60 && g < 60 && b < 60) return false;
        return Math.abs(r - startR) < 60 && Math.abs(g - startG) < 60 && Math.abs(b - startB) < 60;
      }

      const pixelStack = [[startX, startY]];

      while (pixelStack.length) {
        const newPos = pixelStack.pop();
        const x = newPos[0];
        let y = newPos[1];

        let pixelPos = (y * width + x) * 4;

        while (y-- >= 0 && colorMatch(pixelPos)) {
          pixelPos -= width * 4;
        }
        pixelPos += width * 4;
        ++y;

        let reachLeft = false;
        let reachRight = false;

        while (y++ < height - 1 && colorMatch(pixelPos)) {
          data[pixelPos] = fillColor[0];
          data[pixelPos + 1] = fillColor[1];
          data[pixelPos + 2] = fillColor[2];
          data[pixelPos + 3] = 255;

          if (x > 0) {
            if (colorMatch(pixelPos - 4)) {
              if (!reachLeft) {
                pixelStack.push([x - 1, y]);
                reachLeft = true;
              }
            } else if (reachLeft) {
              reachLeft = false;
            }
          }

          if (x < width - 1) {
            if (colorMatch(pixelPos + 4)) {
              if (!reachRight) {
                pixelStack.push([x + 1, y]);
                reachRight = true;
              }
            } else if (reachRight) {
              reachRight = false;
            }
          }

          pixelPos += width * 4;
        }
      }

      ctx.putImageData(imgData, 0, 0);
    }

    function downloadArt() {
      const link = document.createElement('a');
      link.download = `helena-e-betina-arte-pagina-${activePaintIndex}.png`;
      link.href = canvas.toDataURL();
      link.click();
    }

    /* MINI JOGO */
    const gameCanvas = document.getElementById('gameCanvas');
    const gCtx = gameCanvas.getContext('2d');
    
    let gameActive = false;
    let score = 0;
    let lives = 3;
    let selectedChar = 'helena';
    
    let player = { x: 400, y: 300, size: 35 };
    let star = { x: 100, y: 100, size: 25, timer: 100, maxTimer: 100 };
    let sparkles = [];

    const charEmojis = {
      helena: '👩🏼‍🎤',
      betina: '👧🏻',
      unicornio: '🦄',
      lumix: '🪲'
    };

    function selectGameChar(char) {
      selectedChar = char;
      document.querySelectorAll('.char-btn').forEach(b => b.classList.remove('selected'));
      if (char === 'helena') document.getElementById('btnHelena').classList.add('selected');
      if (char === 'betina') document.getElementById('btnBetina').classList.add('selected');
      if (char === 'unicornio') document.getElementById('btnUnicornio').classList.add('selected');
      if (char === 'lumix') document.getElementById('btnLumix').classList.add('selected');
      drawGame();
    }

    function initGame() {
      gameCanvas.width = 800;
      gameCanvas.height = 600;
      player.x = gameCanvas.width / 2;
      player.y = gameCanvas.height / 2;
      drawGame();
      
      gameCanvas.addEventListener('pointermove', (e) => {
        if (!gameActive) return;
        const rect = gameCanvas.getBoundingClientRect();
        player.x = (e.clientX - rect.left) * (gameCanvas.width / rect.width);
        player.y = (e.clientY - rect.top) * (gameCanvas.height / rect.height);
      });
    }

    function spawnStar() {
      star.x = 80 + Math.random() * (gameCanvas.width - 160);
      star.y = 80 + Math.random() * (gameCanvas.height - 180);
      star.maxTimer = Math.max(50, 120 - Math.floor(score / 30) * 10);
      star.timer = star.maxTimer;
    }

    function playSound(type) {
      if (!('AudioContext' in window || 'webkitAudioContext' in window)) return;
      const ctx = new (window.AudioContext || window.webkitAudioContext)();
      const osc = ctx.createOscillator();
      const gain = ctx.createGain();
      
      if (type === 'catch') {
        osc.type = 'sine';
        osc.frequency.setValueAtTime(523.25, ctx.currentTime);
        osc.frequency.exponentialRampToValueAtTime(880, ctx.currentTime + 0.2);
        gain.gain.setValueAtTime(0.2, ctx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + 0.2);
      } else {
        osc.type = 'sawtooth';
        osc.frequency.setValueAtTime(220, ctx.currentTime);
        osc.frequency.exponentialRampToValueAtTime(110, ctx.currentTime + 0.3);
        gain.gain.setValueAtTime(0.3, ctx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + 0.3);
      }
      
      osc.connect(gain);
      gain.connect(ctx.destination);
      osc.start();
      osc.stop(ctx.currentTime + 0.3);
    }

    function updateLivesUI() {
      let hearts = '';
      for (let i = 0; i < lives; i++) hearts += '❤️';
      for (let i = lives; i < 3; i++) hearts += '🖤';
      document.getElementById('gameLives').innerText = hearts;
    }

    function startGame() {
      score = 0;
      lives = 3;
      gameActive = true;
      document.getElementById('gameScore').innerText = score;
      updateLivesUI();
      document.getElementById('btnStartGame').innerText = '🔄 Reiniciar';

      spawnStar();
      gameLoop();
    }

    function createSparkles(x, y) {
      for (let i = 0; i < 15; i++) {
        sparkles.push({
          x: x,
          y: y,
          vx: (Math.random() - 0.5) * 8,
          vy: (Math.random() - 0.5) * 8,
          life: 20,
          color: ['#ffd166', '#ff6b9b', '#a29bfe', '#2ed573'][Math.floor(Math.random() * 4)]
        });
      }
    }

    function updateGame() {
      if (!gameActive) return;

      star.timer--;

      if (star.timer <= 0) {
        lives--;
        updateLivesUI();
        playSound('miss');
        if (lives <= 0) {
          gameActive = false;
          alert(`💔 Ops! A estrela desapareceu! Você fez ${score} pontos. Tente novamente!`);
          drawGame();
          return;
        }
        spawnStar();
      }

      const dist = Math.hypot(player.x - star.x, player.y - star.y);
      if (dist < player.size + star.size) {
        score += 10;
        document.getElementById('gameScore').innerText = score;
        createSparkles(star.x, star.y);
        playSound('catch');
        spawnStar();
      }

      for (let i = sparkles.length - 1; i >= 0; i--) {
        let p = sparkles[i];
        p.x += p.vx;
        p.y += p.vy;
        p.life--;
        if (p.life <= 0) sparkles.splice(i, 1);
      }
    }

    function drawCastleBackground() {
      const bgGrad = gCtx.createLinearGradient(0, 0, 0, gameCanvas.height);
      bgGrad.addColorStop(0, '#12052e');
      bgGrad.addColorStop(0.6, '#31125e');
      bgGrad.addColorStop(1, '#531b78');
      gCtx.fillStyle = bgGrad;
      gCtx.fillRect(0, 0, gameCanvas.width, gameCanvas.height);

      gCtx.save();
      gCtx.fillStyle = '#fffae6';
      gCtx.shadowColor = '#fffae6';
      gCtx.shadowBlur = 20;
      gCtx.beginPath();
      gCtx.arc(700, 90, 45, 0, Math.PI * 2);
      gCtx.fill();
      gCtx.restore();

      gCtx.fillStyle = '#180736';
      gCtx.fillRect(150, 250, 90, 350);
      gCtx.fillRect(560, 250, 90, 350);
      
      gCtx.beginPath();
      gCtx.moveTo(130, 250); gCtx.lineTo(195, 150); gCtx.lineTo(260, 250);
      gCtx.moveTo(540, 250); gCtx.lineTo(605, 150); gCtx.lineTo(670, 250);
      gCtx.fill();

      gCtx.fillRect(310, 180, 180, 420);
      gCtx.beginPath();
      gCtx.moveTo(290, 180); gCtx.lineTo(400, 60); gCtx.lineTo(510, 180);
      gCtx.fill();

      gCtx.fillStyle = '#ffd166';
      gCtx.shadowColor = '#ffd166';
      gCtx.shadowBlur = 10;
      
      gCtx.beginPath();
      gCtx.arc(400, 230, 18, Math.PI, 0);
      gCtx.fillRect(382, 230, 36, 30);
      gCtx.fill();

      gCtx.fillRect(180, 300, 30, 45);
      gCtx.fillRect(590, 300, 30, 45);
      gCtx.restore();

      gCtx.fillStyle = '#0d031f';
      gCtx.beginPath();
      gCtx.arc(400, 600, 55, Math.PI, 0);
      gCtx.fill();

      gCtx.fillStyle = 'rgba(255, 107, 155, 0.25)';
      gCtx.beginPath();
      gCtx.arc(200, 580, 120, 0, Math.PI * 2);
      gCtx.arc(400, 600, 140, 0, Math.PI * 2);
      gCtx.arc(600, 580, 120, 0, Math.PI * 2);
      gCtx.fill();
    }

    function drawGame() {
      drawCastleBackground();

      if (gameActive) {
        gCtx.save();
        gCtx.translate(star.x, star.y);
        
        gCtx.fillStyle = '#ffd166';
        gCtx.shadowColor = '#ffd166';
        gCtx.shadowBlur = 15;
        gCtx.font = '36px sans-serif';
        gCtx.textAlign = 'center';
        gCtx.textBaseline = 'middle';
        gCtx.fillText('⭐', 0, 0);

        const barW = 50;
        const barH = 6;
        const pct = Math.max(0, star.timer / star.maxTimer);
        
        gCtx.shadowBlur = 0;
        gCtx.fillStyle = 'rgba(0,0,0,0.5)';
        gCtx.fillRect(-barW / 2, 25, barW, barH);
        
        gCtx.fillStyle = pct > 0.4 ? '#2ed573' : '#ff4757';
        gCtx.fillRect(-barW / 2, 25, barW * pct, barH);
        
        gCtx.restore();
      }

      sparkles.forEach(p => {
        gCtx.fillStyle = p.color;
        gCtx.beginPath();
        gCtx.arc(p.x, p.y, p.life / 3, 0, Math.PI * 2);
        gCtx.fill();
      });

      gCtx.save();
      gCtx.translate(player.x, player.y);
      
      gCtx.fillStyle = 'rgba(255, 255, 255, 0.4)';
      gCtx.beginPath();
      gCtx.ellipse(-15, -10, 15, 22, Math.PI / 4, 0, Math.PI * 2);
      gCtx.ellipse(15, -10, 15, 22, -Math.PI / 4, 0, Math.PI * 2);
      gCtx.fill();

      gCtx.font = '45px sans-serif';
      gCtx.textAlign = 'center';
      gCtx.textBaseline = 'middle';
      gCtx.fillText(charEmojis[selectedChar], 0, 0);
      
      gCtx.restore();

      if (!gameActive && lives === 3) {
        gCtx.fillStyle = 'rgba(10, 3, 25, 0.65)';
        gCtx.fillRect(0, 0, gameCanvas.width, gameCanvas.height);
        gCtx.fillStyle = '#fff';
        gCtx.font = 'bold 22px Quicksand';
        gCtx.textAlign = 'center';
        gCtx.fillText('Rápido! Pegue as estrelas antes que elas desapareçam!', gameCanvas.width / 2, gameCanvas.height / 2 - 15);
        gCtx.fillStyle = '#ffd166';
        gCtx.font = '18px Quicksand';
        gCtx.fillText('Clique no botão "Iniciar Jogo" para começar!', gameCanvas.width / 2, gameCanvas.height / 2 + 25);
      }
    }

    function gameLoop() {
      if (gameActive) {
        updateGame();
        drawGame();
        requestAnimationFrame(gameLoop);
      }
    }

    renderComicGrid();
  </script>
</body>
</html>
