<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Cuestionario — Teoría General de Diseño Mecánico</title>
  <style>
    :root{
      --bg:#0b1020;
      --card:#111a33;
      --card2:#0f1730;
      --text:#e8ecff;
      --muted:#aeb8e6;
      --accent:#7c5cff;
      --ok:#4ade80;
      --bad:#fb7185;
      --warn:#fbbf24;
      --line:rgba(255,255,255,.10);
      --shadow: 0 16px 50px rgba(0,0,0,.35);
      --radius: 18px;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      background: radial-gradient(1200px 800px at 20% 10%, rgba(124,92,255,.25), transparent 60%),
                  radial-gradient(900px 700px at 90% 30%, rgba(251,113,133,.18), transparent 55%),
                  var(--bg);
      color:var(--text);
      min-height:100vh;
      display:flex;
      align-items:center;
      justify-content:center;
      padding:24px;
    }
    .app{
      width:min(980px, 100%);
      display:grid;
      gap:16px;
    }
    header{
      display:flex;
      align-items:flex-start;
      justify-content:space-between;
      gap:12px;
    }
    .title{
      padding:18px 18px 16px;
      background: linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.03));
      border:1px solid var(--line);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      flex:1;
    }
    .title h1{
      margin:0 0 6px;
      font-size: clamp(18px, 2.3vw, 28px);
      letter-spacing:.2px;
    }
    .title p{
      margin:0;
      color:var(--muted);
      line-height:1.4;
      font-size: 14px;
    }
    .controls{
      display:flex;
      flex-direction:column;
      gap:10px;
      width:min(320px, 100%);
    }
    .pill{
      background: linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.03));
      border:1px solid var(--line);
      border-radius: var(--radius);
      padding:14px;
      box-shadow: var(--shadow);
    }
    .statrow{
      display:flex;
      gap:10px;
      align-items:center;
      justify-content:space-between;
      margin-top:8px;
      flex-wrap:wrap;
    }
    .stat{
      display:flex;
      flex-direction:column;
      gap:2px;
      min-width: 90px;
    }
    .stat b{font-size:16px}
    .stat span{font-size:12px;color:var(--muted)}
    .progress{
      height:10px;
      background: rgba(255,255,255,.06);
      border:1px solid var(--line);
      border-radius: 999px;
      overflow:hidden;
      position:relative;
    }
    .bar{
      height:100%;
      width:0%;
      background: linear-gradient(90deg, var(--accent), rgba(124,92,255,.35));
      transition: width .35s ease;
    }
    main{
      display:grid;
      grid-template-columns: 1.2fr .8fr;
      gap:16px;
    }
    @media (max-width: 880px){
      main{grid-template-columns: 1fr}
      .controls{width:100%}
      header{flex-direction:column}
    }
    .card{
      background: linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.03));
      border:1px solid var(--line);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      overflow:hidden;
    }
    .card .pad{padding:18px}
    .qmeta{
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:10px;
      margin-bottom:12px;
      flex-wrap:wrap;
    }
    .tag{
      font-size:12px;
      color:var(--muted);
      border:1px solid var(--line);
      padding:6px 10px;
      border-radius: 999px;
      background: rgba(0,0,0,.12);
    }
    .question{
      font-size: 18px;
      line-height: 1.35;
      margin: 0 0 14px;
    }
    .choices{
      display:grid;
      gap:10px;
    }
    .choice{
      border:1px solid var(--line);
      background: rgba(0,0,0,.10);
      padding:12px 12px;
      border-radius: 14px;
      cursor:pointer;
      transition: transform .08s ease, border-color .2s ease, background .2s ease;
      display:flex;
      gap:10px;
      align-items:flex-start;
    }
    .choice:hover{transform: translateY(-1px); border-color: rgba(124,92,255,.6)}
    .badge{
      width:28px;height:28px;border-radius:10px;
      display:grid;place-items:center;
      border:1px solid var(--line);
      color:var(--muted);
      flex:0 0 28px;
      background: rgba(255,255,255,.04);
      font-weight:700;
      font-size:13px;
    }
    .choice p{
      margin:0;
      line-height:1.35;
      color: var(--text);
      font-size: 14px;
    }
    .choice[aria-disabled="true"]{cursor:not-allowed; opacity:.9}
    .choice.correct{
      border-color: rgba(74,222,128,.7);
      background: rgba(74,222,128,.08);
    }
    .choice.wrong{
      border-color: rgba(251,113,133,.7);
      background: rgba(251,113,133,.08);
    }
    .feedback{
      margin-top:12px;
      border-top: 1px solid var(--line);
      padding-top:12px;
      display:none;
      animation: pop .2s ease;
    }
    @keyframes pop{from{transform:translateY(3px);opacity:.5}to{transform:translateY(0);opacity:1}}
    .feedback .line{
      display:flex;
      align-items:flex-start;
      gap:10px;
      margin: 6px 0;
      color: var(--muted);
      font-size: 13px;
      line-height: 1.35;
    }
    .dot{
      width:10px;height:10px;border-radius:50%;
      margin-top:4px;
      background: rgba(255,255,255,.20);
      border:1px solid var(--line);
      flex:0 0 10px;
    }
    .dot.ok{background: rgba(74,222,128,.9); border-color: rgba(74,222,128,.4)}
    .dot.bad{background: rgba(251,113,133,.9); border-color: rgba(251,113,133,.4)}
    .actions{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      margin-top:14px;
    }
    button{
      appearance:none;
      border:1px solid var(--line);
      background: rgba(255,255,255,.06);
      color: var(--text);
      padding:10px 12px;
      border-radius: 14px;
      cursor:pointer;
      transition: transform .08s ease, border-color .2s ease, background .2s ease;
      font-weight:650;
      letter-spacing:.1px;
    }
    button:hover{transform: translateY(-1px); border-color: rgba(124,92,255,.6)}
    button.primary{
      background: linear-gradient(90deg, rgba(124,92,255,.95), rgba(124,92,255,.55));
      border-color: rgba(124,92,255,.65);
    }
    button.danger{
      background: rgba(251,113,133,.12);
      border-color: rgba(251,113,133,.45);
    }
    button:disabled{
      opacity:.5; cursor:not-allowed; transform:none;
    }
    .sidebar .pad{display:grid; gap:12px}
    .panel{
      border:1px solid var(--line);
      background: rgba(0,0,0,.10);
      border-radius: 16px;
      padding:12px;
    }
    .panel h3{margin:0 0 6px; font-size:14px}
    .panel p{margin:0; color:var(--muted); font-size:13px; line-height:1.35}
    .mini{
      display:flex; gap:8px; flex-wrap:wrap; margin-top:10px;
    }
    .chip{
      border:1px solid var(--line);
      border-radius: 999px;
      padding:6px 10px;
      font-size:12px;
      color:var(--muted);
      background: rgba(255,255,255,.04);
    }
    .result{
      display:none;
    }
    .result h2{margin:0 0 6px}
    .big{
      font-size: 40px;
      line-height:1;
      margin: 6px 0 10px;
    }
    .meter{
      display:grid;
      gap:10px;
      margin-top:10px;
    }
    .row{
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:10px;
      color:var(--muted);
      font-size:13px;
    }
    .row b{color:var(--text)}
    .kbd{
      font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
      font-size: 12px;
      color: var(--muted);
      border:1px solid var(--line);
      padding:4px 8px;
      border-radius:10px;
      background: rgba(0,0,0,.18);
    }
    .hint{
      margin-top:6px;
      color: var(--muted);
      font-size: 12px;
      line-height:1.35;
    }
  </style>
</head>
<body>
  <div class="app">
    <header>
      <div class="title">
        <h1>Cuestionario interactivo — Teoría general (todos los PDFs)</h1>
        <p>Marca una alternativa por pregunta. Si fallas, verás una explicación breve con la respuesta correcta. Al final se muestran porcentajes de aciertos y fallas.</p>
        <div class="hint">Tip: usa <span class="kbd">1</span> <span class="kbd">2</span> <span class="kbd">3</span> <span class="kbd">4</span> para responder más rápido.</div>
      </div>

      <div class="controls">
        <div class="pill">
          <div class="progress" aria-label="Progreso">
            <div class="bar" id="bar"></div>
          </div>
          <div class="statrow">
            <div class="stat"><b id="idx">1</b><span>Pregunta</span></div>
            <div class="stat"><b id="score">0</b><span>Aciertos</span></div>
            <div class="stat"><b id="fails">0</b><span>Fallas</span></div>
          </div>
        </div>

        <div class="pill">
          <button class="primary" id="btnNext" disabled>Siguiente →</button>
          <div class="actions">
            <button id="btnBack">← Anterior</button>
            <button class="danger" id="btnReset">Reiniciar</button>
          </div>
        </div>
      </div>
    </header>

    <main>
      <section class="card" id="quizCard">
        <div class="pad">
          <div class="qmeta">
            <span class="tag" id="topicTag">Tema</span>
            <span class="tag" id="countTag">1 / 18</span>
          </div>

          <h2 class="question" id="qText">—</h2>

          <div class="choices" id="choices"></div>

          <div class="feedback" id="feedback">
            <div class="line">
              <span class="dot" id="fbDot"></span>
              <div>
                <b id="fbTitle">—</b>
                <div id="fbExplain" style="margin-top:4px;"></div>
              </div>
            </div>
          </div>

          <div class="actions">
            <button id="btnReveal">Ver explicación</button>
          </div>
        </div>
      </section>

      <aside class="card sidebar">
        <div class="pad">
          <div class="panel">
            <h3>¿Qué evalúa este cuestionario?</h3>
            <p>Metodología de diseño, potencia–torque–rpm, torsión/flexión, Von Mises, FS, fatiga, engranajes, rodamientos, fricción/contacto, térmica en frenado, CAE/FEA, TSR/Cp y seguridad por control.</p>
            <div class="mini">
              <span class="chip">Diseño</span>
              <span class="chip">Resistencia</span>
              <span class="chip">Transmisión</span>
              <span class="chip">CAE</span>
              <span class="chip">Seguridad</span>
            </div>
          </div>

          <div class="panel result" id="resultBox">
            <h2>Resultado final</h2>
            <div class="big" id="bigScore">—</div>
            <div class="meter">
              <div class="row"><span>Aciertos</span><b id="okPct">—</b></div>
              <div class="row"><span>Fallas</span><b id="badPct">—</b></div>
              <div class="row"><span>Total</span><b id="totalQ">—</b></div>
            </div>
            <div class="actions" style="margin-top:12px;">
              <button class="primary" id="btnReview">Revisar errores</button>
              <button id="btnRestart2">Reintentar</button>
            </div>
          </div>

          <div class="panel">
            <h3>Modo “pensar”</h3>
            <p>Las alternativas incluyen distractores plausibles (errores típicos). Eso te entrena a no caer en confusiones de unidades, hipótesis y criterios.</p>
          </div>
        </div>
      </aside>
    </main>
  </div>

  <script>
    // === Banco de preguntas (18) ===
    // correct: índice 0..3
    const quiz = [
      {
        topic: "Metodología de diseño",
        q: "¿Qué diferencia clave hay entre requerimientos y criterios de diseño?",
        options: [
          "Requerimientos: lo que debe cumplir; criterios: cómo se mide/valida.",
          "Requerimientos: cálculos finales; criterios: planos de fabricación.",
          "Requerimientos: escoger material; criterios: escoger software.",
          "Requerimientos: siempre cuantitativos; criterios: siempre cualitativos."
        ],
        correct: 0,
        explain: "Requerimientos definen el objetivo/función. Criterios definen la métrica para evaluar si se cumple (seguridad, costo, desempeño, etc.)."
      },
      {
        topic: "Potencia–Torque–RPM",
        q: "Si un motor mantiene potencia constante y la velocidad (rpm) baja, ¿qué ocurre con el torque?",
        options: [
          "Baja el torque porque el motor se “alivia”.",
          "Sube el torque para mantener la potencia.",
          "Torque no cambia porque depende del material del eje.",
          "El torque se vuelve cero si la rpm baja mucho."
        ],
        correct: 1,
        explain: "P = T·ω. Si P es constante y ω baja, entonces T debe subir."
      },
      {
        topic: "Unidades y errores típicos",
        q: "¿Cuál es el error más peligroso al convertir potencia y rpm para hallar torque?",
        options: [
          "Usar siempre HP en lugar de kW.",
          "Confundir rpm con rad/s y no controlar unidades.",
          "Redondear el resultado final.",
          "Usar demasiados decimales."
        ],
        correct: 1,
        explain: "El error clásico es mezclar rpm con rad/s o HP con kW sin conversión, lo que cambia el torque y dimensiona mal todo."
      },
      {
        topic: "Torsión + Flexión",
        q: "¿Por qué un eje real rara vez trabaja en torsión pura?",
        options: [
          "Porque siempre hay flexión por fuerzas, peso, poleas, desalineación o reacciones.",
          "Porque la torsión solo existe en ejes huecos.",
          "Porque la flexión se elimina si el material es AISI 4140.",
          "Porque la torsión no se considera en máquinas industriales."
        ],
        correct: 0,
        explain: "En operación aparecen fuerzas radiales, pesos y desalineación; eso genera momentos flectores además del torque."
      },
      {
        topic: "Esfuerzos combinados",
        q: "Si hay flexión (σ) y torsión (τ) al mismo tiempo, ¿qué criterio se usa típicamente para materiales dúctiles?",
        options: [
          "Coulomb-Mohr, porque siempre es más seguro.",
          "Von Mises, para esfuerzo equivalente.",
          "Solo comparar σ con Sy y olvidar τ.",
          "Usar únicamente presión de contacto."
        ],
        correct: 1,
        explain: "Von Mises combina σ y τ en un esfuerzo equivalente para comparar con el límite de fluencia en materiales dúctiles."
      },
      {
        topic: "Factor de seguridad",
        q: "¿Qué justifica realmente un factor de seguridad (FS)?",
        options: [
          "Que el diseño quede más bonito y simétrico.",
          "Cubrir incertidumbres: cargas reales, material, fabricación, impactos, errores.",
          "Evitar usar normas técnicas.",
          "Asegurar que nunca exista deformación."
        ],
        correct: 1,
        explain: "FS cubre incertidumbres del mundo real. No significa 'sin deformación', sino margen ante variabilidad."
      },
      {
        topic: "FS en práctica",
        q: "¿Por qué no conviene elegir siempre un FS “muy alto” sin análisis?",
        options: [
          "Porque reduce la vida a fatiga automáticamente.",
          "Porque sube peso/costo y puede empeorar eficiencia sin necesidad.",
          "Porque hace que la pieza sea frágil por definición.",
          "Porque elimina la necesidad de ensayos."
        ],
        correct: 1,
        explain: "FS demasiado alto puede sobredimensionar: más masa, costo, consumo y problemas de manufactura sin beneficio real."
      },
      {
        topic: "Fatiga",
        q: "¿Cómo puede fallar una pieza “segura en estático”?",
        options: [
          "Por falta de color en el recubrimiento.",
          "Por fatiga: daño acumulado por ciclos repetidos.",
          "Porque Von Mises solo se aplica a aceros.",
          "Porque el torque nunca se repite."
        ],
        correct: 1,
        explain: "La fatiga depende de ciclos. Una tensión repetida por miles/millones de ciclos puede generar grietas y falla."
      },
      {
        topic: "Goodman",
        q: "En términos simples, ¿qué combina el criterio de Goodman?",
        options: [
          "Esfuerzo medio + esfuerzo alternante en un límite de seguridad.",
          "Temperatura + presión para evitar desgaste.",
          "Potencia + eficiencia del motor.",
          "Rigidez + masa para evitar vibración."
        ],
        correct: 0,
        explain: "Goodman relaciona esfuerzo alternante y medio con resistencia última/límite de fatiga para evitar falla por ciclos."
      },
      {
        topic: "Engranajes / Reducción",
        q: "Una relación de transmisión i = 21 significa:",
        options: [
          "La salida gira 21 veces más rápido.",
          "La salida gira 21 veces más lenta (idealmente más torque).",
          "El torque de salida se divide entre 21.",
          "La potencia se multiplica por 21."
        ],
        correct: 1,
        explain: "i>1 en reductor: se reduce velocidad y se incrementa torque (idealmente), con potencia casi conservada menos pérdidas."
      },
      {
        topic: "Etapas de reducción",
        q: "¿Por qué se usan dos etapas para reducciones grandes?",
        options: [
          "Porque una sola etapa no transmite torque.",
          "Para repartir cargas/tamaños y mejorar diseño/eficiencia.",
          "Porque Von Mises lo exige.",
          "Para evitar usar rodamientos."
        ],
        correct: 1,
        explain: "Dos etapas permiten engranes razonables en tamaño y esfuerzos, evitando engranes gigantes o cargas excesivas."
      },
      {
        topic: "Rodamientos (L10)",
        q: "¿Qué representa L10 en rodamientos?",
        options: [
          "La vida a la que 10% falla y 90% sobrevive (confiabilidad 90%).",
          "La vida mínima garantizada para 100% de rodamientos.",
          "El número de dientes del engrane.",
          "La longitud del eje en pulgadas."
        ],
        correct: 0,
        explain: "L10 es la vida estadística: 90% de rodamientos sobreviven a esa vida bajo condiciones especificadas."
      },
      {
        topic: "Rodamientos en realidad",
        q: "¿Qué causa típica hace que una vida L10 teórica NO se cumpla?",
        options: [
          "Usar un catálogo SKF en PDF.",
          "Lubricación deficiente, contaminación, desalineación, montaje incorrecto.",
          "Tener FS alto.",
          "Calcular torque en kW."
        ],
        correct: 1,
        explain: "La vida real cae por lubricación/contaminación/desalineación/instalación. Son factores dominantes en campo."
      },
      {
        topic: "Fricción (freno)",
        q: "En un freno de disco, el torque de frenado aumenta si:",
        options: [
          "Aumentas μ, o la fuerza normal, o el radio medio efectivo.",
          "Bajas μ para evitar desgaste.",
          "Reduces el radio medio para “concentrar” la fuerza.",
          "El área aumenta siempre, sin importar el resto."
        ],
        correct: 0,
        explain: "Modelo básico: T = μ·F·Rm. Subir cualquiera de esos tres aumenta T."
      },
      {
        topic: "Fricción (gripper)",
        q: "En un gripper con dos mordazas, ¿por qué aparece el “2” en Fs ≥ W/(2μ)?",
        options: [
          "Porque el peso se divide entre dos puntos de contacto.",
          "Porque μ siempre vale 2 en antideslizantes.",
          "Porque el torque de motor se duplica automáticamente.",
          "Porque se asume gravedad doble."
        ],
        correct: 0,
        explain: "Dos mordazas aportan fricción. Cada una aporta una parte del soporte del peso."
      },
      {
        topic: "Térmica en frenado",
        q: "¿Qué se convierte principalmente en calor durante el frenado?",
        options: [
          "Energía cinética (y/o potencial) del sistema.",
          "Esfuerzo equivalente Von Mises.",
          "Relación de transmisión i.",
          "Vida L10 del rodamiento."
        ],
        correct: 0,
        explain: "En frenado, energía mecánica se disipa como calor; si no se gestiona, sube temperatura y cambia comportamiento."
      },
      {
        topic: "CAE/FEA",
        q: "¿Qué diferencia práctica hay entre dimensionar y verificar con FEA?",
        options: [
          "FEA reemplaza todas las normas, por eso basta con simular.",
          "Cálculo dimensiona; FEA verifica deformaciones, picos y zonas críticas.",
          "FEA solo sirve para hacer renders.",
          "Dimensionar solo se usa en eólica."
        ],
        correct: 1,
        explain: "Primero se dimensiona con teoría. Luego FEA verifica distribución real, concentraciones y deformaciones."
      },
      {
        topic: "Eólica (TSR/Cp)",
        q: "Si el TSR real está muy por debajo del TSR óptimo, lo más probable es:",
        options: [
          "Que el rotor extraiga menos potencia (opera lejos del punto eficiente).",
          "Que Cp sea máximo automáticamente.",
          "Que la potencia no dependa del viento.",
          "Que el radio medio del freno aumente."
        ],
        correct: 0,
        explain: "Cada rotor tiene TSR óptimo. Muy por debajo suele indicar operación ineficiente y menor potencia extraída."
      }
    ];

    // === Estado ===
    let i = 0;
    const answers = Array(quiz.length).fill(null); // {picked, correct, shownExplain}
    let locked = false;

    // === DOM ===
    const qText = document.getElementById("qText");
    const choices = document.getElementById("choices");
    const topicTag = document.getElementById("topicTag");
    const countTag = document.getElementById("countTag");
    const idx = document.getElementById("idx");
    const score = document.getElementById("score");
    const fails = document.getElementById("fails");
    const bar = document.getElementById("bar");
    const btnNext = document.getElementById("btnNext");
    const btnBack = document.getElementById("btnBack");
    const btnReset = document.getElementById("btnReset");
    const btnReveal = document.getElementById("btnReveal");

    const feedback = document.getElementById("feedback");
    const fbDot = document.getElementById("fbDot");
    const fbTitle = document.getElementById("fbTitle");
    const fbExplain = document.getElementById("fbExplain");

    const resultBox = document.getElementById("resultBox");
    const bigScore = document.getElementById("bigScore");
    const okPct = document.getElementById("okPct");
    const badPct = document.getElementById("badPct");
    const totalQ = document.getElementById("totalQ");
    const btnReview = document.getElementById("btnReview");
    const btnRestart2 = document.getElementById("btnRestart2");

    function tally(){
      let ok = 0, bad = 0;
      for(const a of answers){
        if(!a) continue;
        if(a.correct) ok++;
        else bad++;
      }
      score.textContent = ok;
      fails.textContent = bad;
      return {ok, bad};
    }

    function setProgress(){
      const done = answers.filter(a => a !== null).length;
      const pct = Math.round((done / quiz.length) * 100);
      bar.style.width = pct + "%";
      idx.textContent = (i+1);
      countTag.textContent = `${i+1} / ${quiz.length}`;
      topicTag.textContent = quiz[i].topic;
    }

    function showFeedback(a){
      if(!a) { feedback.style.display="none"; return; }
      feedback.style.display = "block";
      if(a.correct){
        fbDot.className = "dot ok";
        fbTitle.textContent = "Correcto";
        fbExplain.textContent = "Bien. Sigue con la siguiente pregunta.";
      } else {
        fbDot.className = "dot bad";
        fbTitle.textContent = "Incorrecto — explicación";
        fbExplain.textContent = quiz[i].explain;
      }
    }

    function render(){
      locked = false;
      btnNext.disabled = true;
      resultBox.style.display = "none";

      const item = quiz[i];
      qText.textContent = item.q;
      choices.innerHTML = "";

      const letters = ["A","B","C","D"];
      item.options.forEach((opt, k) => {
        const div = document.createElement("div");
        div.className = "choice";
        div.setAttribute("role","button");
        div.tabIndex = 0;

        div.innerHTML = `<span class="badge">${letters[k]}</span><p>${opt}</p>`;
        div.addEventListener("click", () => pick(k));
        div.addEventListener("keydown", (e) => {
          if(e.key === "Enter" || e.key === " ") pick(k);
        });
        choices.appendChild(div);
      });

      setProgress();
      tally();

      // Si ya respondió esta pregunta, mostrar estado
      if(answers[i]){
        applyAnswerState();
      } else {
        feedback.style.display="none";
      }

      btnBack.disabled = i === 0;
      btnReveal.disabled = answers[i] ? false : true;
    }

    function applyAnswerState(){
      const item = quiz[i];
      const a = answers[i];
      const nodes = [...choices.children];
      nodes.forEach((node, k) => {
        node.setAttribute("aria-disabled","true");
        node.classList.remove("correct","wrong");
        if(k === item.correct) node.classList.add("correct");
        if(!a.correct && k === a.picked) node.classList.add("wrong");
      });
      btnNext.disabled = (i === quiz.length-1) ? false : false;
      locked = true;
      showFeedback(a);
      btnReveal.disabled = false;
      btnNext.textContent = (i === quiz.length-1) ? "Ver resultado →" : "Siguiente →";
    }

    function pick(k){
      if(locked) return;
      const item = quiz[i];
      const isOk = (k === item.correct);
      answers[i] = { picked: k, correct: isOk };
      applyAnswerState();
      tally();
    }

    function next(){
      if(!answers[i]) return;
      if(i < quiz.length-1){
        i++;
        render();
      } else {
        showResults();
      }
    }

    function back(){
      if(i > 0){
        i--;
        render();
      }
    }

    function reset(){
      i = 0;
      for(let j=0;j<answers.length;j++) answers[j] = null;
      btnNext.textContent = "Siguiente →";
      render();
    }

    function showResults(){
      const {ok, bad} = tally();
      const total = quiz.length;
      const okP = Math.round((ok/total)*100);
      const badP = 100 - okP;

      bigScore.textContent = `${ok} / ${total}`;
      okPct.textContent = `${okP}%`;
      badPct.textContent = `${badP}%`;
      totalQ.textContent = `${total} preguntas`;

      resultBox.style.display = "block";
      btnNext.disabled = true;
      // desplazar a resultado
      resultBox.scrollIntoView({behavior:"smooth", block:"start"});
    }

    function reviewErrors(){
      // Ir a la primera pregunta fallada
      const idxBad = answers.findIndex(a => a && !a.correct);
      if(idxBad === -1){
        alert("No tienes errores. ¡Perfecto!");
        return;
      }
      i = idxBad;
      render();
    }

    // Atajos numéricos 1..4
    window.addEventListener("keydown", (e) => {
      if(resultBox.style.display === "block") return;
      if(["1","2","3","4"].includes(e.key)){
        const k = parseInt(e.key,10)-1;
        pick(k);
      }
    });

    btnNext.addEventListener("click", next);
    btnBack.addEventListener("click", back);
    btnReset.addEventListener("click", reset);
    btnReveal.addEventListener("click", () => {
      if(!answers[i]) return;
      // Si está correcto, mostrar mini feedback; si está mal, explicación ya está
      showFeedback(answers[i]);
      feedback.scrollIntoView({behavior:"smooth", block:"nearest"});
    });
    btnReview.addEventListener("click", reviewErrors);
    btnRestart2.addEventListener("click", reset);

    render();
  </script>
</body>
</html>
