<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Cuestionario — Teoría General (55 preguntas)</title>
  <style>
    :root{
      --bg:#0b1020; --card:#111a33; --text:#e8ecff; --muted:#aeb8e6;
      --accent:#7c5cff; --ok:#4ade80; --bad:#fb7185; --line:rgba(255,255,255,.10);
      --shadow: 0 16px 50px rgba(0,0,0,.35); --radius: 18px;
    }
    *{box-sizing:border-box}
    body{
      margin:0; font-family: system-ui,-apple-system,Segoe UI,Roboto,Arial,sans-serif;
      background:
        radial-gradient(1200px 800px at 20% 10%, rgba(124,92,255,.25), transparent 60%),
        radial-gradient(900px 700px at 90% 30%, rgba(251,113,133,.18), transparent 55%),
        var(--bg);
      color:var(--text); min-height:100vh; display:flex; align-items:center; justify-content:center; padding:24px;
    }
    .app{width:min(1100px, 100%); display:grid; gap:16px;}
    header{display:flex; align-items:flex-start; justify-content:space-between; gap:12px;}
    .title{
      padding:18px; background: linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.03));
      border:1px solid var(--line); border-radius: var(--radius); box-shadow: var(--shadow); flex:1;
    }
    .title h1{margin:0 0 6px; font-size: clamp(18px, 2.2vw, 28px); letter-spacing:.2px;}
    .title p{margin:0; color:var(--muted); line-height:1.4; font-size:14px;}
    .hint{margin-top:8px; color:var(--muted); font-size:12px; line-height:1.35;}
    .kbd{font-family: ui-monospace,SFMono-Regular,Menlo,Consolas,monospace; font-size:12px; color:var(--muted);
      border:1px solid var(--line); padding:4px 8px; border-radius:10px; background: rgba(0,0,0,.18);}
    .controls{display:flex; flex-direction:column; gap:10px; width:min(360px, 100%);}
    .pill{
      background: linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.03));
      border:1px solid var(--line); border-radius: var(--radius); padding:14px; box-shadow: var(--shadow);
    }
    .progress{height:10px; background: rgba(255,255,255,.06); border:1px solid var(--line); border-radius:999px; overflow:hidden;}
    .bar{height:100%; width:0%; background: linear-gradient(90deg, var(--accent), rgba(124,92,255,.35)); transition: width .35s ease;}
    .statrow{display:flex; gap:10px; align-items:center; justify-content:space-between; margin-top:10px; flex-wrap:wrap;}
    .stat{display:flex; flex-direction:column; gap:2px; min-width: 90px;}
    .stat b{font-size:16px} .stat span{font-size:12px;color:var(--muted)}
    main{display:grid; grid-template-columns: 1.15fr .85fr; gap:16px;}
    @media (max-width: 900px){ main{grid-template-columns:1fr} header{flex-direction:column} .controls{width:100%} }
    .card{
      background: linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.03));
      border:1px solid var(--line); border-radius: var(--radius); box-shadow: var(--shadow); overflow:hidden;
    }
    .pad{padding:18px}
    .qmeta{display:flex; align-items:center; justify-content:space-between; gap:10px; margin-bottom:12px; flex-wrap:wrap;}
    .tag{
      font-size:12px; color:var(--muted); border:1px solid var(--line);
      padding:6px 10px; border-radius:999px; background: rgba(0,0,0,.12);
    }
    .question{font-size:18px; line-height:1.35; margin:0 0 14px;}
    .choices{display:grid; gap:10px;}
    .choice{
      border:1px solid var(--line); background: rgba(0,0,0,.10);
      padding:12px; border-radius:14px; cursor:pointer;
      transition: transform .08s ease, border-color .2s ease, background .2s ease;
      display:flex; gap:10px; align-items:flex-start;
    }
    .choice:hover{transform: translateY(-1px); border-color: rgba(124,92,255,.6)}
    .badge{
      width:28px;height:28px;border-radius:10px; display:grid; place-items:center;
      border:1px solid var(--line); color:var(--muted); flex:0 0 28px;
      background: rgba(255,255,255,.04); font-weight:800; font-size:13px;
    }
    .choice p{margin:0; line-height:1.35; color:var(--text); font-size:14px;}
    .choice[aria-disabled="true"]{cursor:not-allowed; opacity:.95}
    .choice.correct{border-color: rgba(74,222,128,.7); background: rgba(74,222,128,.08);}
    .choice.wrong{border-color: rgba(251,113,133,.7); background: rgba(251,113,133,.08);}
    .feedback{
      margin-top:12px; border-top:1px solid var(--line); padding-top:12px;
      display:none; animation: pop .2s ease;
    }
    @keyframes pop{from{transform:translateY(3px);opacity:.5}to{transform:translateY(0);opacity:1}}
    .line{display:flex; align-items:flex-start; gap:10px; margin:6px 0; color:var(--muted); font-size:13px; line-height:1.35;}
    .dot{width:10px;height:10px;border-radius:50%; margin-top:4px; background: rgba(255,255,255,.2); border:1px solid var(--line); flex:0 0 10px;}
    .dot.ok{background: rgba(74,222,128,.9); border-color: rgba(74,222,128,.4)}
    .dot.bad{background: rgba(251,113,133,.9); border-color: rgba(251,113,133,.4)}
    .actions{display:flex; gap:10px; flex-wrap:wrap; margin-top:14px;}
    button{
      appearance:none; border:1px solid var(--line); background: rgba(255,255,255,.06);
      color: var(--text); padding:10px 12px; border-radius:14px;
      cursor:pointer; transition: transform .08s ease, border-color .2s ease, background .2s ease;
      font-weight:700; letter-spacing:.1px;
    }
    button:hover{transform: translateY(-1px); border-color: rgba(124,92,255,.6)}
    button.primary{background: linear-gradient(90deg, rgba(124,92,255,.95), rgba(124,92,255,.55)); border-color: rgba(124,92,255,.65);}
    button.danger{background: rgba(251,113,133,.12); border-color: rgba(251,113,133,.45);}
    button:disabled{opacity:.55; cursor:not-allowed; transform:none;}
    .panel{border:1px solid var(--line); background: rgba(0,0,0,.10); border-radius:16px; padding:12px;}
    .panel h3{margin:0 0 6px; font-size:14px}
    .panel p{margin:0; color:var(--muted); font-size:13px; line-height:1.35}
    .mini{display:flex; gap:8px; flex-wrap:wrap; margin-top:10px;}
    .chip{border:1px solid var(--line); border-radius:999px; padding:6px 10px; font-size:12px; color:var(--muted); background: rgba(255,255,255,.04);}
    .result{display:none;}
    .result h2{margin:0 0 6px}
    .big{font-size:42px; line-height:1; margin: 6px 0 10px;}
    .meter{display:grid; gap:10px; margin-top:10px;}
    .row{display:flex; align-items:center; justify-content:space-between; gap:10px; color:var(--muted); font-size:13px;}
    .row b{color:var(--text)}
    .modeRow{display:flex; gap:10px; flex-wrap:wrap; align-items:center; justify-content:space-between; margin-top:10px;}
    .toggle{
      display:flex; gap:10px; align-items:center; justify-content:space-between;
      border:1px solid var(--line); background: rgba(0,0,0,.10);
      padding:10px 12px; border-radius:14px;
    }
    .toggle label{color:var(--muted); font-size:13px}
    .toggle input{transform: scale(1.1);}
  </style>
</head>

<body>
  <div class="app">
    <header>
      <div class="title">
        <h1>Cuestionario interactivo — Teoría general (55 preguntas)</h1>
        <p>Incluye <b>todas</b> las preguntas en el mismo orden que pediste (1→55, por temas). Muestra % de aciertos/fallas al final y explica cuando te equivocas.</p>
        <div class="hint">
          Atajos: <span class="kbd">1</span> <span class="kbd">2</span> <span class="kbd">3</span> <span class="kbd">4</span>.
          Modo examen: oculta si está bien/mal hasta el final.
        </div>
      </div>

      <div class="controls">
        <div class="pill">
          <div class="progress" aria-label="Progreso"><div class="bar" id="bar"></div></div>
          <div class="statrow">
            <div class="stat"><b id="idx">1</b><span>Pregunta</span></div>
            <div class="stat"><b id="score">0</b><span>Aciertos</span></div>
            <div class="stat"><b id="fails">0</b><span>Fallas</span></div>
          </div>
          <div class="modeRow">
            <div class="toggle" title="Si activas Modo examen, no verás si estuvo bien o mal hasta el final.">
              <label for="examMode">Modo examen</label>
              <input id="examMode" type="checkbox" />
            </div>
            <div class="toggle" title="Si activas Aleatorio, se barajan preguntas y opciones (mantiene contenido).">
              <label for="shuffleMode">Aleatorio</label>
              <input id="shuffleMode" type="checkbox" />
            </div>
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
            <span class="tag" id="countTag">1 / 55</span>
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

      <aside class="card">
        <div class="pad" style="display:grid; gap:12px;">
          <div class="panel">
            <h3>Qué mide</h3>
            <p>Diseño sistemático, energía de máquinas, esfuerzos combinados, FS, fatiga, transmisión, rodamientos, fricción, térmica, CAE/FEA, aerodinámica y seguridad por control.</p>
            <div class="mini">
              <span class="chip">Diseño</span><span class="chip">Resistencia</span><span class="chip">Transmisión</span>
              <span class="chip">CAE</span><span class="chip">Seguridad</span>
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
            <h3>Cómo se corrige</h3>
            <p>En modo normal: feedback inmediato y explicación si fallas. En modo examen: todo se muestra al final.</p>
          </div>
        </div>
      </aside>
    </main>
  </div>

  <script>
    // ============================================================
    // 55 preguntas EXACTAMENTE en el orden y por temas como pediste
    // ============================================================
    const baseQuiz = [
      // 1) Metodología de diseño
      {topic:"1) Metodología de diseño", q:"1. ¿Cuál es la diferencia entre requerimientos (qué debe hacer) y criterios de diseño (cómo se evaluará)?",
        options:[
          "Requerimientos: lo que debe cumplir; criterios: cómo se mide/valida.",
          "Requerimientos: cálculos finales; criterios: planos de fabricación.",
          "Requerimientos: el software a usar; criterios: el material a usar.",
          "Requerimientos: siempre cualitativos; criterios: siempre cuantitativos."
        ], correct:0,
        explain:"Requerimientos definen la función/objetivo. Criterios son las métricas para evaluar (seguridad, costo, desempeño, etc.)."
      },
      {topic:"1) Metodología de diseño", q:"2. ¿Qué etapas mínimas debe tener un proceso de diseño sistemático desde la necesidad hasta la validación?",
        options:[
          "Necesidad → requisitos → conceptos → selección → diseño → verificación → documentación.",
          "Necesidad → comprar materiales → fabricar → vender.",
          "Modelar en CAD → imprimir planos → listo.",
          "Simular primero → recién definir requisitos."
        ], correct:0,
        explain:"Un proceso mínimo incluye: definir requisitos, proponer conceptos, seleccionar, diseñar y verificar/validar."
      },
      {topic:"1) Metodología de diseño", q:"3. ¿Cómo construirías una matriz tipo VDI 2225 para priorizar seguridad y mantenimiento?",
        options:[
          "Criterios + pesos + puntaje por alternativa; dar mayor peso a seguridad/mantenimiento.",
          "Elegir la alternativa más barata sin ponderación.",
          "Sumar solo la potencia del motor y ya.",
          "Comparar solo estética y tamaño."
        ], correct:0,
        explain:"VDI 2225 se apoya en criterios ponderados y puntajes comparables entre alternativas."
      },
      {topic:"1) Metodología de diseño", q:"4. ¿Qué significa “comparación técnico–económica” y qué riesgo hay si solo comparas costo?",
        options:[
          "Comparar desempeño y costos; riesgo: elegir barato pero inseguro/ineficiente.",
          "Comparar solo marcas y disponibilidad; riesgo: demoras.",
          "Comparar solo planos; riesgo: errores de dibujo.",
          "Comparar solo peso; riesgo: vibración."
        ], correct:0,
        explain:"Técnico–económica = desempeño + costo total. Solo costo puede ocultar riesgos operativos."
      },
      {topic:"1) Metodología de diseño", q:"5. ¿Cuándo una alternativa “gana” aunque sea más cara?",
        options:[
          "Cuando mejora seguridad, confiabilidad o reduce paradas/mantenimiento.",
          "Cuando tiene más piezas.",
          "Cuando usa un material más raro.",
          "Cuando aumenta la complejidad de control."
        ], correct:0,
        explain:"Puede ganar por costo de ciclo de vida: menos fallas, más seguridad, mejor mantenimiento."
      },

      // 2) Potencia–torque–velocidad
      {topic:"2) Potencia–Torque–RPM", q:"6. Si un motor entrega potencia constante y baja la rpm, ¿qué pasa con el torque?",
        options:[
          "Sube el torque para mantener potencia.",
          "Baja el torque necesariamente.",
          "No cambia porque depende del diámetro del eje.",
          "Se vuelve cero si baja la rpm."
        ], correct:0,
        explain:"P = T·ω. Si P es constante y ω baja, T debe subir."
      },
      {topic:"2) Potencia–Torque–RPM", q:"7. ¿Cómo obtienes torque a partir de HP y rpm, y qué debes cuidar?",
        options:[
          "Convertir unidades (HP→kW o usar fórmula consistente) y no mezclar rpm con rad/s.",
          "Sumar HP con rpm y dividir entre 2.",
          "Multiplicar HP por rpm sin conversión.",
          "Usar Von Mises para hallar torque."
        ], correct:0,
        explain:"El punto crítico es coherencia de unidades (P, n, ω)."
      },
      {topic:"2) Potencia–Torque–RPM", q:"8. ¿Por qué un error en rpm puede sobredimensionar o subdimensionar ejes/engranajes?",
        options:[
          "Porque el torque calculado depende inversamente de la velocidad para una potencia dada.",
          "Porque el material cambia con la rpm automáticamente.",
          "Porque el CAD falla si la rpm es alta.",
          "Porque los rodamientos no dependen del torque."
        ], correct:0,
        explain:"Con potencia dada, T ~ 1/ω. Error de rpm cambia T y por tanto esfuerzos."
      },
      {topic:"2) Potencia–Torque–RPM", q:"9. En un sistema con reductor, ¿qué cambia y qué no cambia idealmente?",
        options:[
          "Cambian rpm y torque; la potencia se conserva casi (menos pérdidas).",
          "No cambia nada: rpm y torque quedan iguales.",
          "Solo cambia la potencia; rpm y torque se mantienen.",
          "Cambia el material del eje automáticamente."
        ], correct:0,
        explain:"Idealmente P≈constante, mientras n baja y T sube según relación."
      },

      // 3) Torsión + flexión
      {topic:"3) Resistencia (torsión/flexión)", q:"10. ¿Por qué un eje real casi nunca trabaja con torsión pura?",
        options:[
          "Porque además del torque hay fuerzas radiales que generan flexión.",
          "Porque la torsión solo existe en ejes macizos.",
          "Porque la flexión se elimina con acero 4140.",
          "Porque el torque es despreciable en máquinas."
        ], correct:0,
        explain:"Pesos, poleas, engranes, desalineación y reacciones generan momentos flectores."
      },
      {topic:"3) Resistencia (torsión/flexión)", q:"11. ¿Cuál es el origen físico del momento flector y del torque en una máquina?",
        options:[
          "Flexión: fuerzas; torsión: potencia transmitida (par).",
          "Flexión: temperatura; torsión: presión de contacto.",
          "Flexión: vida L10; torsión: Cp eólico.",
          "Flexión: CAD; torsión: PLC."
        ], correct:0,
        explain:"M proviene de fuerzas aplicadas; T proviene del par que transmite energía."
      },
      {topic:"3) Resistencia (torsión/flexión)", q:"12. ¿Qué efecto tiene aumentar el diámetro del eje en el esfuerzo por torsión?",
        options:[
          "Disminuye fuertemente (aprox. proporcional a 1/d³).",
          "Aumenta linealmente.",
          "No cambia.",
          "Solo cambia si el eje es hueco."
        ], correct:0,
        explain:"Para eje circular macizo: τ ~ T·r/J y J ~ d⁴ ⇒ τ ~ 1/d³."
      },
      {topic:"3) Resistencia (torsión/flexión)", q:"13. ¿Cómo identificas la sección crítica de un eje con varias cargas?",
        options:[
          "Donde el momento/torque es máximo y/o hay cambios de sección (concentración).",
          "Donde el eje tiene pintura.",
          "Siempre en el centro geométrico.",
          "Donde la rpm es menor."
        ], correct:0,
        explain:"La sección crítica suele coincidir con máximos de M/T y discontinuidades geométricas."
      },

      // 4) Von Mises
      {topic:"4) Esfuerzos combinados (Von Mises)", q:"14. ¿Por qué no basta comparar σ (flexión) con Sy cuando también hay τ (torsión)?",
        options:[
          "Porque el estado real es combinado y puede fallar aunque σ sola sea baja.",
          "Porque Sy no existe en aceros.",
          "Porque τ no genera esfuerzos.",
          "Porque Von Mises solo se usa en FEA."
        ], correct:0,
        explain:"Debes usar un criterio equivalente (p.ej., Von Mises) que combine σ y τ."
      },
      {topic:"4) Esfuerzos combinados (Von Mises)", q:"15. ¿Qué representa físicamente el esfuerzo equivalente Von Mises?",
        options:[
          "Un esfuerzo único equivalente al estado combinado para comparar con fluencia.",
          "La presión de contacto promedio.",
          "La temperatura máxima del freno.",
          "La relación de transmisión."
        ], correct:0,
        explain:"Permite comparar un estado multiaxial con el límite de fluencia de materiales dúctiles."
      },
      {topic:"4) Esfuerzos combinados (Von Mises)", q:"16. ¿En qué materiales es más apropiado Von Mises y por qué?",
        options:[
          "En dúctiles, porque modela bien la fluencia por energía de distorsión.",
          "En frágiles, porque ignora la tracción.",
          "En polímeros, porque siempre da FS=∞.",
          "En cualquier material, porque reemplaza ensayos."
        ], correct:0,
        explain:"Von Mises es estándar para materiales dúctiles (aceros, aluminios)."
      },
      {topic:"4) Esfuerzos combinados (Von Mises)", q:"17. Si Von Mises da “seguro” pero la pieza falla, ¿qué hipótesis pudo estar mal?",
        options:[
          "Cargas/BC incorrectas, concentraciones, fatiga, material real o montaje distinto.",
          "Que Von Mises sea una marca de software.",
          "Que el torque no exista en la realidad.",
          "Que la gravedad sea menor."
        ], correct:0,
        explain:"Fallos típicos vienen de entrada incorrecta o modo de falla distinto (fatiga, impacto, etc.)."
      },

      // 5) FS
      {topic:"5) Factor de seguridad", q:"18. ¿Qué incertidumbres reales cubre el factor de seguridad?",
        options:[
          "Variación de carga, material, fabricación, montaje, impactos y errores.",
          "Solo el color de pintura.",
          "Solo el tipo de CAD.",
          "Solo la marca del rodamiento."
        ], correct:0,
        explain:"FS incorpora incertidumbre del mundo real y dispersión de parámetros."
      },
      {topic:"5) Factor de seguridad", q:"19. ¿Por qué FS no debe ser “lo más alto posible” sin análisis?",
        options:[
          "Porque puede subir costo/peso y empeorar eficiencia sin necesidad.",
          "Porque reduce la potencia del motor a cero.",
          "Porque hace al material más frágil por definición.",
          "Porque elimina la necesidad de mantenimiento."
        ], correct:0,
        explain:"Sobredimensionar trae penalizaciones (masa, costo, manufactura) sin beneficio proporcional."
      },
      {topic:"5) Factor de seguridad", q:"20. ¿Cómo elegirías FS para grúa, gripper ligero y eje de mezclador?",
        options:[
          "Grúa: alto; gripper: medio; eje mezclador: medio-alto por ciclos/impactos.",
          "Todos iguales siempre.",
          "Gripper: el más alto; grúa: el más bajo.",
          "Depende solo del color del material."
        ], correct:0,
        explain:"FS depende de riesgo, consecuencias de falla, variabilidad de carga y fatiga."
      },
      {topic:"5) Factor de seguridad", q:"21. ¿Qué implica tener FS=1.2 vs FS=3 en costo y confiabilidad?",
        options:[
          "1.2: poco margen; 3: más confiable pero más pesado/caro.",
          "1.2: siempre más seguro; 3: siempre inseguro.",
          "Ambos son equivalentes.",
          "FS no se relaciona con confiabilidad."
        ], correct:0,
        explain:"Mayor FS suele aumentar confiabilidad ante incertidumbre, pero también costo/peso."
      },

      // 6) Fatiga
      {topic:"6) Fatiga (Goodman)", q:"22. ¿Por qué una pieza puede fallar por fatiga aunque en estático sea “segura”?",
        options:[
          "Por daño acumulado por ciclos repetidos.",
          "Porque el esfuerzo estático nunca importa.",
          "Porque el material pierde masa.",
          "Porque la rpm elimina esfuerzos."
        ], correct:0,
        explain:"La fatiga depende del número de ciclos y amplitud de esfuerzos."
      },
      {topic:"6) Fatiga (Goodman)", q:"23. ¿Qué diferencia hay entre esfuerzo medio y esfuerzo alternante?",
        options:[
          "Medio: componente constante; alternante: variación cíclica.",
          "Medio: por fricción; alternante: por temperatura.",
          "Medio: por CAD; alternante: por PLC.",
          "No hay diferencia real."
        ], correct:0,
        explain:"En fatiga, σm desplaza el ciclo y σa es la amplitud del ciclo."
      },
      {topic:"6) Fatiga (Goodman)", q:"24. ¿Qué representa la línea de Goodman en términos de seguridad?",
        options:[
          "El límite de combinaciones (σa, σm) aceptables para evitar falla por fatiga.",
          "La curva de temperatura del freno.",
          "La relación de transmisión óptima.",
          "La vida L10 del rodamiento."
        ], correct:0,
        explain:"Goodman define una frontera de diseño entre seguro y no seguro bajo carga cíclica."
      },
      {topic:"6) Fatiga (Goodman)", q:"25. ¿Qué datos mínimos necesitas para un chequeo de fatiga realista?",
        options:[
          "σa, σm y propiedades de fatiga/resistencia del material (con factores).",
          "Solo Sy.",
          "Solo Cp y TSR.",
          "Solo potencia del motor."
        ], correct:0,
        explain:"Se necesita caracterizar el ciclo y las propiedades (Se, Su) y factores (superficie, tamaño, etc.)."
      },
      {topic:"6) Fatiga (Goodman)", q:"26. ¿Qué cambia si hay concentraciones de esfuerzo (chaveteros, filetes)?",
        options:[
          "Sube el esfuerzo local y baja la vida a fatiga.",
          "Baja el esfuerzo local y sube la vida.",
          "No cambia nada en fatiga.",
          "Solo afecta temperatura."
        ], correct:0,
        explain:"Los concentradores elevan tensiones locales y facilitan iniciación de grietas."
      },

      // 7) Engranajes
      {topic:"7) Engranajes / relación i", q:"27. ¿Qué significa una relación i=21 en un reductor?",
        options:[
          "La salida gira 21 veces más lenta que la entrada.",
          "La salida gira 21 veces más rápida.",
          "La potencia se multiplica por 21 sin pérdidas.",
          "El torque se divide por 21."
        ], correct:0,
        explain:"Un reductor con i>1 reduce velocidad; idealmente incrementa torque."
      },
      {topic:"7) Engranajes / relación i", q:"28. Si reduces rpm, ¿qué ocurre con el torque a la salida idealmente?",
        options:[
          "Aumenta proporcionalmente a la relación de reducción (menos pérdidas).",
          "Disminuye necesariamente.",
          "Se vuelve independiente de la carga.",
          "Solo depende del diámetro del eje."
        ], correct:0,
        explain:"Con potencia aproximadamente constante, al bajar ω aumenta T."
      },
      {topic:"7) Engranajes / relación i", q:"29. ¿Por qué se usan 2 etapas para reducciones grandes?",
        options:[
          "Para repartir cargas/tamaños y evitar engranes extremos en una sola etapa.",
          "Porque una sola etapa nunca funciona.",
          "Porque elimina la necesidad de rodamientos.",
          "Porque la norma lo prohíbe siempre."
        ], correct:0,
        explain:"Dos etapas permiten engranes razonables, menos esfuerzos y mejor integración."
      },
      {topic:"7) Engranajes / relación i", q:"30. ¿Qué consecuencias tiene una relación de transmisión mal calculada en una cinta transportadora?",
        options:[
          "No cumple velocidad/torque, puede sobrecargar, patinar o fallar por calentamiento.",
          "Solo cambia el color del tambor.",
          "Solo afecta el PLC, no lo mecánico.",
          "No tiene ninguna consecuencia."
        ], correct:0,
        explain:"i afecta rpm y torque: si está mal, el sistema no cumple la función o se sobrecarga."
      },

      // 8) Rodamientos
      {topic:"8) Rodamientos (L10)", q:"31. ¿Qué es L10 y qué significa “90% de confiabilidad”?",
        options:[
          "Vida a la que 90% sobrevive y 10% falla bajo condiciones especificadas.",
          "Vida garantizada para 100%.",
          "La longitud del eje en mm.",
          "La carga estática del rodamiento."
        ], correct:0,
        explain:"Es una vida estadística: 90% de rodamientos llega a esa vida."
      },
      {topic:"8) Rodamientos (L10)", q:"32. ¿Por qué se usa carga equivalente P si hay cargas combinadas?",
        options:[
          "Para representar un caso equivalente que produce el mismo daño que las cargas reales combinadas.",
          "Para evitar calcular fuerzas.",
          "Para aumentar artificialmente la vida.",
          "Porque P es siempre igual a C."
        ], correct:0,
        explain:"P combina componentes radial/axial en una sola carga de referencia para vida."
      },
      {topic:"8) Rodamientos (L10)", q:"33. ¿Qué puede hacer que una vida teórica enorme no se cumpla en operación real?",
        options:[
          "Lubricación deficiente, contaminación, desalineación, montaje, golpes, temperatura.",
          "Usar un catálogo en PDF.",
          "Tener el eje pintado.",
          "Que la potencia esté en kW."
        ], correct:0,
        explain:"Los factores de campo dominan la falla real, mucho más que la vida teórica."
      },
      {topic:"8) Rodamientos (L10)", q:"34. ¿Cómo afecta desalineamiento y mala lubricación a la vida del rodamiento?",
        options:[
          "La reduce drásticamente por aumento de carga local y fricción/calor.",
          "La aumenta porque “se acomoda”.",
          "No afecta la vida.",
          "Solo afecta el ruido, no la vida."
        ], correct:0,
        explain:"Genera cargas localizadas, desgaste, temperatura y falla prematura."
      },

      // 9) Fricción y contacto
      {topic:"9) Fricción y contacto", q:"35. En un freno de disco, ¿qué variables aumentan el torque de frenado?",
        options:[
          "Aumentar μ, F normal o Rm (radio medio efectivo).",
          "Reducir μ para frenar más.",
          "Reducir Rm para aumentar torque.",
          "Aumentar la rpm para frenar más."
        ], correct:0,
        explain:"Modelo base: T = μ·F·Rm."
      },
      {topic:"9) Fricción y contacto", q:"36. ¿Por qué aparece Rm (radio medio) y qué pasa si cambias Di y Do?",
        options:[
          "Porque el esfuerzo de fricción se distribuye en el anillo; Di/Do cambia el radio efectivo y el torque.",
          "Porque Rm es constante siempre.",
          "Porque solo importa el área, no el radio.",
          "Porque Rm depende del PLC."
        ], correct:0,
        explain:"El par depende del brazo efectivo de fricción: cambiar geometría cambia Rm y el torque."
      },
      {topic:"9) Fricción y contacto", q:"37. En un gripper, ¿por qué Fs ≥ W/(2μ)? ¿Qué representa el “2”?",
        options:[
          "Dos mordazas comparten el peso: cada una aporta fricción.",
          "Porque μ vale 2 por norma.",
          "Porque la gravedad se duplica por seguridad.",
          "Porque el objeto pesa el doble en operación."
        ], correct:0,
        explain:"El peso se sostiene por fricción en dos contactos; cada contacto aporta parte."
      },
      {topic:"9) Fricción y contacto", q:"38. ¿Qué riesgo hay si asumes un μ demasiado alto sin validarlo?",
        options:[
          "Que el objeto deslice o el freno no alcance el torque real requerido.",
          "Que aumente automáticamente la potencia del motor.",
          "Que desaparezca la presión de contacto.",
          "Que la vida L10 siempre suba."
        ], correct:0,
        explain:"μ sobredimensionado en el papel puede fallar en práctica (contaminación, desgaste, humedad)."
      },
      {topic:"9) Fricción y contacto", q:"39. ¿Cómo se relacionan p = F/A y desgaste?",
        options:[
          "Mayor p suele aumentar desgaste y riesgo térmico/daño superficial.",
          "Mayor p siempre reduce desgaste.",
          "El desgaste no depende de p.",
          "p solo afecta rodamientos, no frenos."
        ], correct:0,
        explain:"Presión alta incrementa esfuerzos de contacto, temperatura y desgaste (dependiendo material/velocidad)."
      },

      // 10) Térmica en frenado
      {topic:"10) Térmica en frenado", q:"40. ¿Qué energía se transforma en calor durante un frenado?",
        options:[
          "Energía cinética (y/o potencial) del sistema.",
          "Esfuerzo equivalente Von Mises.",
          "Relación de transmisión i.",
          "Vida L10."
        ], correct:0,
        explain:"La disipación principal es de energía mecánica a calor por fricción."
      },
      {topic:"10) Térmica en frenado", q:"41. ¿Qué factores controlan la temperatura máxima alcanzada?",
        options:[
          "Energía por frenada, tiempo, capacidad térmica, ventilación, área y materiales.",
          "Solo el color del disco.",
          "Solo el límite de fluencia Sy.",
          "Solo la potencia del PLC."
        ], correct:0,
        explain:"Tmax depende de energía/tiempo de disipación y capacidades de conducción/convección."
      },
      {topic:"10) Térmica en frenado", q:"42. ¿Por qué el análisis térmico es clave para seguridad en industria?",
        options:[
          "Porque evita sobrecalentamiento, pérdida de fricción, degradación y riesgos operativos.",
          "Porque reemplaza el cálculo mecánico.",
          "Porque hace innecesaria la ventilación.",
          "Porque reduce la gravedad."
        ], correct:0,
        explain:"Un freno puede fallar por temperatura aunque resista mecánicamente."
      },
      {topic:"10) Térmica en frenado", q:"43. ¿Qué significa el factor de partición de calor η y por qué no es 1?",
        options:[
          "Es la fracción de calor que absorbe un componente; el resto se va al otro/ambiente.",
          "Es el coeficiente de fricción.",
          "Es la vida L10.",
          "Es la relación de transmisión."
        ], correct:0,
        explain:"El calor se reparte entre disco/pastillas/entorno; no todo lo absorbe un solo elemento."
      },

      // 11) CAE/FEA
      {topic:"11) CAE / FEA", q:"44. ¿Qué diferencia hay entre “dimensionar” con cálculos y “verificar” con FEA?",
        options:[
          "Cálculo define tamaños; FEA valida distribución, picos y deformaciones con condiciones de borde.",
          "FEA reemplaza normas y cálculos siempre.",
          "Dimensionar solo sirve para eólica.",
          "FEA solo sirve para renders."
        ], correct:0,
        explain:"FEA es verificación; el dimensionamiento inicial viene de teoría/normas."
      },
      {topic:"11) CAE / FEA", q:"45. ¿Qué condiciones de borde mal puestas pueden falsear resultados de esfuerzo?",
        options:[
          "Empotramientos irreales, cargas mal aplicadas, contactos mal definidos.",
          "Elegir fuente de letra incorrecta.",
          "Usar demasiados decimales.",
          "Modelar en mm en lugar de m (si todo está consistente)."
        ], correct:0,
        explain:"BC/contacts dominan tensiones; un apoyo irreal altera picos y rigidez global."
      },
      {topic:"11) CAE / FEA", q:"46. ¿Cómo usarías FEA para detectar concentraciones de esfuerzo?",
        options:[
          "Revisar mapas de tensión y picos en cambios de sección, filetes, agujeros, uniones.",
          "Mirar solo el peso del modelo.",
          "Desactivar contactos para acelerar.",
          "No mallar: usar malla 1 elemento."
        ], correct:0,
        explain:"Las concentraciones aparecen en discontinuidades geométricas y contactos."
      },
      {topic:"11) CAE / FEA", q:"47. Si el desplazamiento es grande pero los esfuerzos son bajos, ¿qué puede estar pasando?",
        options:[
          "Problema de rigidez/BC, material mal asignado o estructura flexible aunque no exceda Sy.",
          "Que Von Mises sea inválido.",
          "Que la fricción sea negativa.",
          "Que la rpm sea cero."
        ], correct:0,
        explain:"Puedes estar en zona elástica con tensiones moderadas pero rigidez insuficiente (deflexión funcionalmente inaceptable)."
      },

      // 12) Eólica (Cp y TSR)
      {topic:"12) Eólica (Cp/TSR)", q:"48. ¿Qué es Cp y qué significa físicamente?",
        options:[
          "Coeficiente de potencia: fracción de energía del viento convertida en potencia útil.",
          "Coeficiente de presión de contacto del freno.",
          "Ciclo de vida L10 del rodamiento.",
          "Relación de transmisión de engranes."
        ], correct:0,
        explain:"Cp mide eficiencia aerodinámica de conversión de energía del viento."
      },
      {topic:"12) Eólica (Cp/TSR)", q:"49. ¿Qué es TSR y por qué existe un TSR óptimo?",
        options:[
          "Relación velocidad punta / velocidad viento; hay óptimo por aerodinámica del rotor.",
          "Temperatura superficial del rotor; hay óptimo por pintura.",
          "Torque/área; hay óptimo por costo.",
          "Tensión equivalente; hay óptimo por norma."
        ], correct:0,
        explain:"Cada geometría tiene punto de operación donde maximiza Cp."
      },
      {topic:"12) Eólica (Cp/TSR)", q:"50. Si TSR real es muy bajo respecto al óptimo, ¿qué implica en potencia extraída?",
        options:[
          "Menor potencia (opera lejos del punto eficiente).",
          "Mayor potencia automáticamente.",
          "Potencia independiente del viento.",
          "Que el freno disipa menos calor."
        ], correct:0,
        explain:"Lejos del TSR óptimo, Cp cae y se extrae menos potencia."
      },
      {topic:"12) Eólica (Cp/TSR)", q:"51. ¿Qué variables geométricas cambian el desempeño de un Savonius?",
        options:[
          "Radio, solape, forma/número de palas, altura y proporciones.",
          "Solo el color del rotor.",
          "Solo el tipo de rodamiento.",
          "Solo el PLC del sistema."
        ], correct:0,
        explain:"La geometría define arrastre/retorno y por tanto torque, Cp y TSR."
      },

      // 13) Automatización y seguridad
      {topic:"13) Automatización y seguridad", q:"52. ¿Qué es un enclavamiento y por qué se usa para evitar movimientos peligrosos?",
        options:[
          "Bloqueo lógico/eléctrico que impide acciones incompatibles (p.ej. invertir a la vez).",
          "Un tornillo más grande para aguantar carga.",
          "Un lubricante especial.",
          "Una simulación de Von Mises."
        ], correct:0,
        explain:"Interlocks evitan comandos simultáneos o secuencias inseguras."
      },
      {topic:"13) Automatización y seguridad", q:"53. ¿Por qué los finales de carrera son críticos en una grúa?",
        options:[
          "Evitan sobre-recorridos, choques y daños estructurales por exceder límites.",
          "Solo sirven para estética del tablero.",
          "Solo para aumentar rpm.",
          "Porque reemplazan los frenos."
        ], correct:0,
        explain:"Limit switches detienen movimiento en extremos para prevenir colisiones y sobrecarga."
      },
      {topic:"13) Automatización y seguridad", q:"54. ¿Qué diferencia hay entre seguridad estructural y seguridad operativa?",
        options:[
          "Estructural: no colapsa; operativa: control evita accidentes por maniobras/errores.",
          "Estructural: PLC; operativa: material.",
          "Estructural: rodamientos; operativa: engranes.",
          "No hay diferencia."
        ], correct:0,
        explain:"La estructura puede ser fuerte, pero sin control y protecciones, la operación puede ser peligrosa."
      },
      {topic:"13) Automatización y seguridad", q:"55. ¿Qué puede pasar si automatizas sin protección contra sobrecarga?",
        options:[
          "Falla mecánica/eléctrica, daño por exceder capacidad y riesgo de accidente.",
          "Mejora automática de la vida L10.",
          "Desaparece el calentamiento del freno.",
          "Se multiplica la potencia sin límites."
        ], correct:0,
        explain:"Sin protección, el sistema puede forzar cargas fuera de diseño."
      },
    ];

    // ====== Estado ======
    let quiz = [];
    let mapIndex = [];            // para rastrear índice original si se baraja
    let i = 0;
    let answers = [];             // {picked, correct}
    let locked = false;

    // ====== DOM ======
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
    const examMode = document.getElementById("examMode");
    const shuffleMode = document.getElementById("shuffleMode");

    function clone(obj){ return JSON.parse(JSON.stringify(obj)); }

    function shuffleArray(a){
      for(let j=a.length-1;j>0;j--){
        const k = Math.floor(Math.random()*(j+1));
        [a[j], a[k]] = [a[k], a[j]];
      }
      return a;
    }

    function buildQuiz(){
      // Construir quiz (posible barajado) y reiniciar estado
      quiz = clone(baseQuiz);
      mapIndex = quiz.map((_, idx)=>idx);

      if(shuffleMode.checked){
        // barajar preguntas
        const zipped = quiz.map((q, idx)=>({q, idx}));
        shuffleArray(zipped);
        quiz = zipped.map(z=>z.q);
        mapIndex = zipped.map(z=>z.idx);

        // barajar opciones por pregunta conservando correct
        quiz.forEach(item=>{
          const zippedOpt = item.options.map((t, idx)=>({t, idx}));
          shuffleArray(zippedOpt);
          item.options = zippedOpt.map(z=>z.t);
          item.correct = zippedOpt.findIndex(z=>z.idx === item.correct);
        });
      }

      i = 0;
      answers = Array(quiz.length).fill(null);
      btnNext.textContent = "Siguiente →";
      render();
    }

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
      if(examMode.checked){
        feedback.style.display = "none";
        return;
      }
      if(!a){ feedback.style.display="none"; return; }
      feedback.style.display = "block";
      if(a.correct){
        fbDot.className = "dot ok";
        fbTitle.textContent = "Correcto";
        fbExplain.textContent = "Bien. Puedes continuar.";
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

      if(answers[i]){
        applyAnswerState();
      } else {
        feedback.style.display="none";
      }

      btnBack.disabled = i === 0;
      btnReveal.disabled = !answers[i];
    }

    function applyAnswerState(){
      const item = quiz[i];
      const a = answers[i];
      const nodes = [...choices.children];
      nodes.forEach((node, k) => {
        node.setAttribute("aria-disabled","true");
        node.classList.remove("correct","wrong");
        if(!examMode.checked){
          if(k === item.correct) node.classList.add("correct");
          if(!a.correct && k === a.picked) node.classList.add("wrong");
        }
      });
      locked = true;
      showFeedback(a);
      btnReveal.disabled = false;
      btnNext.disabled = false;
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
      buildQuiz();
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
      resultBox.scrollIntoView({behavior:"smooth", block:"start"});
    }

    function reviewErrors(){
      const idxBad = answers.findIndex(a => a && !a.correct);
      if(idxBad === -1){ alert("No tienes errores. ¡Excelente!"); return; }
      examMode.checked = false; // para ver explicación al revisar
      i = idxBad;
      render();
      // en revisión, mostrar colores aunque estuviera en examen
      if(answers[i]) applyAnswerState();
    }

    // Atajos 1..4 (solo si no está en resultados)
    window.addEventListener("keydown", (e) => {
      if(resultBox.style.display === "block") return;
      if(["1","2","3","4"].includes(e.key)){
        pick(parseInt(e.key,10)-1);
      }
    });

    // Botones
    btnNext.addEventListener("click", next);
    btnBack.addEventListener("click", back);
    btnReset.addEventListener("click", reset);
    btnReveal.addEventListener("click", () => {
      if(!answers[i]) return;
      // En examen no se muestra explicación hasta el final
      if(examMode.checked){
        alert("Modo examen activado: las correcciones se ven al final. Desactívalo si quieres feedback inmediato.");
        return;
      }
      showFeedback(answers[i]);
      feedback.scrollIntoView({behavior:"smooth", block:"nearest"});
    });
    btnReview.addEventListener("click", reviewErrors);
    btnRestart2.addEventListener("click", reset);

    // Cambios de modo (reinicia para coherencia)
    examMode.addEventListener("change", () => {
      // no reinicia, solo cambia comportamiento de feedback
      if(answers[i]) applyAnswerState(); else render();
    });
    shuffleMode.addEventListener("change", () => buildQuiz());

    // Init
    buildQuiz();
  </script>
</body>
</html>
