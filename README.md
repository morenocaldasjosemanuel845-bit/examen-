<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Cuestionario — Teoría General (55 preguntas)</title>
  <style>
    :root{
      --bg:#0b1020; --text:#e8ecff; --muted:#aeb8e6; --accent:#7c5cff;
      --line:rgba(255,255,255,.10); --shadow: 0 16px 50px rgba(0,0,0,.35); --radius:18px;
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
    .title h1{margin:0 0 6px; font-size: clamp(18px, 2.2vw, 28px);}
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
    .tag{font-size:12px; color:var(--muted); border:1px solid var(--line); padding:6px 10px; border-radius:999px; background: rgba(0,0,0,.12);}
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
      font-weight:700;
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
    .toggle{display:flex; gap:10px; align-items:center; justify-content:space-between;
      border:1px solid var(--line); background: rgba(0,0,0,.10);
      padding:10px 12px; border-radius:14px;}
    .toggle label{color:var(--muted); font-size:13px}
    .toggle input{transform: scale(1.1);}
  </style>
</head>

<body>
  <div class="app">
    <header>
      <div class="title">
        <h1>Cuestionario interactivo — Teoría general (55 preguntas)</h1>
        <p>Alternativas “para pensar”, respuestas distribuidas (no siempre A). Si fallas, aparece explicación. Al final: % aciertos y % fallas.</p>
        <div class="hint">
          Atajos: <span class="kbd">1</span> <span class="kbd">2</span> <span class="kbd">3</span> <span class="kbd">4</span>.
        </div>
      </div>

      <div class="controls">
        <div class="pill">
          <div class="progress"><div class="bar" id="bar"></div></div>
          <div class="statrow">
            <div class="stat"><b id="idx">1</b><span>Pregunta</span></div>
            <div class="stat"><b id="score">0</b><span>Aciertos</span></div>
            <div class="stat"><b id="fails">0</b><span>Fallas</span></div>
          </div>
          <div class="modeRow">
            <div class="toggle">
              <label for="examMode">Modo examen</label>
              <input id="examMode" type="checkbox" />
            </div>
            <div class="toggle">
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
      <section class="card">
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
            <h3>Tips</h3>
            <p>Las respuestas están repartidas entre A/B/C/D. No busques patrones. Lee con calma: hay distractores típicos (unidades, hipótesis, criterios).</p>
            <div class="mini">
              <span class="chip">Unidades</span><span class="chip">Hipótesis</span><span class="chip">FS</span><span class="chip">Fatiga</span><span class="chip">CAE</span>
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
            <h3>Modo examen</h3>
            <p>Oculta corrección hasta el final. Útil para practicar sin pistas.</p>
          </div>
        </div>
      </aside>
    </main>
  </div>

  <script>
    // ============================================================
    // 55 preguntas (en el orden original). Respuestas NO siempre A.
    // Nota: Las opciones están reordenadas para que el correcto
    // quede repartido entre A/B/C/D de forma "confusa".
    // ============================================================
    const baseQuiz = [
      // 1) Metodología de diseño
      {topic:"1) Metodología de diseño", q:"1. ¿Cuál es la diferencia entre requerimientos (qué debe hacer) y criterios de diseño (cómo se evaluará)?",
        options:[
          "Requerimientos: cálculos finales; criterios: planos de fabricación.",
          "Requerimientos: lo que debe cumplir; criterios: cómo se mide/valida.",
          "Requerimientos: el software a usar; criterios: el material a usar.",
          "Requerimientos: siempre cualitativos; criterios: siempre cuantitativos."
        ], correct:1,
        explain:"Requerimientos definen función/objetivo. Criterios son métricas de evaluación (seguridad, costo, desempeño, etc.)."
      },
      {topic:"1) Metodología de diseño", q:"2. ¿Qué etapas mínimas debe tener un proceso de diseño sistemático desde la necesidad hasta la validación?",
        options:[
          "Necesidad → comprar materiales → fabricar → vender.",
          "Modelar en CAD → imprimir planos → listo.",
          "Necesidad → requisitos → conceptos → selección → diseño → verificación → documentación.",
          "Simular primero → recién definir requisitos."
        ], correct:2,
        explain:"Secuencia mínima: definir requisitos, proponer conceptos, seleccionar, diseñar y verificar/validar."
      },
      {topic:"1) Metodología de diseño", q:"3. ¿Cómo construirías una matriz tipo VDI 2225 para priorizar seguridad y mantenimiento?",
        options:[
          "Elegir la alternativa más barata sin ponderación.",
          "Comparar solo estética y tamaño.",
          "Criterios + pesos + puntaje por alternativa; dar mayor peso a seguridad/mantenimiento.",
          "Sumar solo la potencia del motor y ya."
        ], correct:2,
        explain:"VDI 2225 usa criterios ponderados y puntajes por alternativa."
      },
      {topic:"1) Metodología de diseño", q:"4. ¿Qué significa “comparación técnico–económica” y qué riesgo hay si solo comparas costo?",
        options:[
          "Comparar solo marcas y disponibilidad; riesgo: demoras.",
          "Comparar desempeño y costos; riesgo: elegir barato pero inseguro/ineficiente.",
          "Comparar solo planos; riesgo: errores de dibujo.",
          "Comparar solo peso; riesgo: vibración."
        ], correct:1,
        explain:"Técnico–económica = desempeño + costo total. Solo costo oculta riesgos operativos."
      },
      {topic:"1) Metodología de diseño", q:"5. ¿Cuándo una alternativa “gana” aunque sea más cara?",
        options:[
          "Cuando aumenta la complejidad de control.",
          "Cuando tiene más piezas.",
          "Cuando mejora seguridad, confiabilidad o reduce paradas/mantenimiento.",
          "Cuando usa un material más raro."
        ], correct:2,
        explain:"Gana por costo de ciclo de vida: menos fallas, mayor seguridad, mejor mantenimiento."
      },

      // 2) Potencia–torque–velocidad
      {topic:"2) Potencia–Torque–RPM", q:"6. Si un motor entrega potencia constante y baja la rpm, ¿qué pasa con el torque?",
        options:[
          "No cambia porque depende del diámetro del eje.",
          "Sube el torque para mantener potencia.",
          "Baja el torque necesariamente.",
          "Se vuelve cero si baja la rpm."
        ], correct:1,
        explain:"P = T·ω. Si P es constante y ω baja, T sube."
      },
      {topic:"2) Potencia–Torque–RPM", q:"7. ¿Cómo obtienes torque a partir de HP y rpm, y qué debes cuidar?",
        options:[
          "Sumar HP con rpm y dividir entre 2.",
          "Multiplicar HP por rpm sin conversión.",
          "Convertir unidades (HP→kW o fórmula consistente) y no mezclar rpm con rad/s.",
          "Usar Von Mises para hallar torque."
        ], correct:2,
        explain:"Clave: consistencia de unidades (P, n, ω)."
      },
      {topic:"2) Potencia–Torque–RPM", q:"8. ¿Por qué un error en rpm puede sobredimensionar o subdimensionar ejes/engranajes?",
        options:[
          "Porque el torque calculado depende inversamente de la velocidad para una potencia dada.",
          "Porque los rodamientos no dependen del torque.",
          "Porque el material cambia con la rpm automáticamente.",
          "Porque el CAD falla si la rpm es alta."
        ], correct:0,
        explain:"Con potencia dada, T ~ 1/ω. Error de rpm cambia T y esfuerzos."
      },
      {topic:"2) Potencia–Torque–RPM", q:"9. En un sistema con reductor, ¿qué cambia y qué no cambia idealmente?",
        options:[
          "No cambia nada: rpm y torque quedan iguales.",
          "Cambia el material del eje automáticamente.",
          "Cambian rpm y torque; la potencia se conserva casi (menos pérdidas).",
          "Solo cambia la potencia; rpm y torque se mantienen."
        ], correct:2,
        explain:"Idealmente P≈constante, n baja y T sube."
      },

      // 3) Torsión + flexión
      {topic:"3) Resistencia (torsión/flexión)", q:"10. ¿Por qué un eje real casi nunca trabaja con torsión pura?",
        options:[
          "Porque además del torque hay fuerzas radiales que generan flexión.",
          "Porque la torsión solo existe en ejes macizos.",
          "Porque el torque es despreciable en máquinas.",
          "Porque la flexión se elimina con acero 4140."
        ], correct:0,
        explain:"Pesos, poleas, engranes, desalineación generan momentos flectores."
      },
      {topic:"3) Resistencia (torsión/flexión)", q:"11. ¿Cuál es el origen físico del momento flector y del torque en una máquina?",
        options:[
          "Flexión: vida L10; torsión: Cp eólico.",
          "Flexión: fuerzas; torsión: potencia transmitida (par).",
          "Flexión: CAD; torsión: PLC.",
          "Flexión: temperatura; torsión: presión de contacto."
        ], correct:1,
        explain:"M proviene de fuerzas; T proviene del par de transmisión de energía."
      },
      {topic:"3) Resistencia (torsión/flexión)", q:"12. ¿Qué efecto tiene aumentar el diámetro del eje en el esfuerzo por torsión?",
        options:[
          "Disminuye fuertemente (aprox. proporcional a 1/d³).",
          "Aumenta linealmente.",
          "Solo cambia si el eje es hueco.",
          "No cambia."
        ], correct:0,
        explain:"Para eje macizo: τ ~ 1/d³."
      },
      {topic:"3) Resistencia (torsión/flexión)", q:"13. ¿Cómo identificas la sección crítica de un eje con varias cargas?",
        options:[
          "Donde la rpm es menor.",
          "Siempre en el centro geométrico.",
          "Donde el momento/torque es máximo y/o hay cambios de sección (concentración).",
          "Donde el eje tiene pintura."
        ], correct:2,
        explain:"Coincide con máximos de M/T y discontinuidades geométricas."
      },

      // 4) Von Mises
      {topic:"4) Esfuerzos combinados (Von Mises)", q:"14. ¿Por qué no basta comparar σ (flexión) con Sy cuando también hay τ (torsión)?",
        options:[
          "Porque Sy no existe en aceros.",
          "Porque el estado real es combinado y puede fallar aunque σ sola sea baja.",
          "Porque τ no genera esfuerzos.",
          "Porque Von Mises solo se usa en FEA."
        ], correct:1,
        explain:"Se necesita criterio equivalente que combine σ y τ."
      },
      {topic:"4) Esfuerzos combinados (Von Mises)", q:"15. ¿Qué representa físicamente el esfuerzo equivalente Von Mises?",
        options:[
          "La relación de transmisión.",
          "Un esfuerzo único equivalente al estado combinado para comparar con fluencia.",
          "La temperatura máxima del freno.",
          "La presión de contacto promedio."
        ], correct:1,
        explain:"Permite comparar un estado multiaxial con el límite de fluencia."
      },
      {topic:"4) Esfuerzos combinados (Von Mises)", q:"16. ¿En qué materiales es más apropiado Von Mises y por qué?",
        options:[
          "En polímeros, porque siempre da FS=∞.",
          "En dúctiles, porque modela la fluencia por energía de distorsión.",
          "En frágiles, porque ignora la tracción.",
          "En cualquier material, porque reemplaza ensayos."
        ], correct:1,
        explain:"Es estándar para materiales dúctiles."
      },
      {topic:"4) Esfuerzos combinados (Von Mises)", q:"17. Si Von Mises da “seguro” pero la pieza falla, ¿qué hipótesis pudo estar mal?",
        options:[
          "Que Von Mises sea una marca de software.",
          "Que la gravedad sea menor.",
          "Cargas/BC incorrectas, concentraciones, fatiga, material real o montaje distinto.",
          "Que el torque no exista en la realidad."
        ], correct:2,
        explain:"Fallos típicos vienen de entradas/BC incorrectas o modo de falla distinto (fatiga, impacto, etc.)."
      },

      // 5) FS
      {topic:"5) Factor de seguridad", q:"18. ¿Qué incertidumbres reales cubre el factor de seguridad?",
        options:[
          "Solo la marca del rodamiento.",
          "Variación de carga, material, fabricación, montaje, impactos y errores.",
          "Solo el color de pintura.",
          "Solo el tipo de CAD."
        ], correct:1,
        explain:"FS incorpora incertidumbre del mundo real."
      },
      {topic:"5) Factor de seguridad", q:"19. ¿Por qué FS no debe ser “lo más alto posible” sin análisis?",
        options:[
          "Porque puede subir costo/peso y empeorar eficiencia sin necesidad.",
          "Porque elimina la necesidad de mantenimiento.",
          "Porque hace al material más frágil por definición.",
          "Porque reduce la potencia del motor a cero."
        ], correct:0,
        explain:"Sobredimensionar trae penalizaciones sin beneficio proporcional."
      },
      {topic:"5) Factor de seguridad", q:"20. ¿Cómo elegirías FS para grúa, gripper ligero y eje de mezclador?",
        options:[
          "Depende solo del color del material.",
          "Todos iguales siempre.",
          "Grúa: alto; gripper: medio; eje mezclador: medio-alto por ciclos/impactos.",
          "Gripper: el más alto; grúa: el más bajo."
        ], correct:2,
        explain:"FS depende de riesgo y variabilidad de carga, y fatiga."
      },
      {topic:"5) Factor de seguridad", q:"21. ¿Qué implica tener FS=1.2 vs FS=3 en costo y confiabilidad?",
        options:[
          "FS no se relaciona con confiabilidad.",
          "1.2: poco margen; 3: más confiable pero más pesado/caro.",
          "1.2: siempre más seguro; 3: siempre inseguro.",
          "Ambos son equivalentes."
        ], correct:1,
        explain:"Mayor FS suele aumentar confiabilidad ante incertidumbre, con costo/peso mayores."
      },

      // 6) Fatiga
      {topic:"6) Fatiga (Goodman)", q:"22. ¿Por qué una pieza puede fallar por fatiga aunque en estático sea “segura”?",
        options:[
          "Porque el material pierde masa.",
          "Porque el esfuerzo estático nunca importa.",
          "Por daño acumulado por ciclos repetidos.",
          "Porque la rpm elimina esfuerzos."
        ], correct:2,
        explain:"Fatiga depende de ciclos y amplitud de esfuerzos."
      },
      {topic:"6) Fatiga (Goodman)", q:"23. ¿Qué diferencia hay entre esfuerzo medio y esfuerzo alternante?",
        options:[
          "Medio: por CAD; alternante: por PLC.",
          "No hay diferencia real.",
          "Medio: componente constante; alternante: variación cíclica.",
          "Medio: por fricción; alternante: por temperatura."
        ], correct:2,
        explain:"σm es el nivel medio y σa es la amplitud del ciclo."
      },
      {topic:"6) Fatiga (Goodman)", q:"24. ¿Qué representa la línea de Goodman en términos de seguridad?",
        options:[
          "La vida L10 del rodamiento.",
          "El límite de combinaciones (σa, σm) aceptables para evitar falla por fatiga.",
          "La curva de temperatura del freno.",
          "La relación de transmisión óptima."
        ], correct:1,
        explain:"Define frontera de diseño entre seguro y no seguro bajo carga cíclica."
      },
      {topic:"6) Fatiga (Goodman)", q:"25. ¿Qué datos mínimos necesitas para un chequeo de fatiga realista?",
        options:[
          "Solo Sy.",
          "Solo Cp y TSR.",
          "σa, σm y propiedades de fatiga/resistencia del material (con factores).",
          "Solo potencia del motor."
        ], correct:2,
        explain:"Se necesita ciclo (σa, σm) y propiedades (Se, Su) + factores."
      },
      {topic:"6) Fatiga (Goodman)", q:"26. ¿Qué cambia si hay concentraciones de esfuerzo (chaveteros, filetes)?",
        options:[
          "Solo afecta temperatura.",
          "Sube el esfuerzo local y baja la vida a fatiga.",
          "No cambia nada en fatiga.",
          "Baja el esfuerzo local y sube la vida."
        ], correct:1,
        explain:"Los concentradores elevan tensiones locales y favorecen grietas."
      },

      // 7) Engranajes
      {topic:"7) Engranajes / relación i", q:"27. ¿Qué significa una relación i=21 en un reductor?",
        options:[
          "La salida gira 21 veces más rápida.",
          "La potencia se multiplica por 21 sin pérdidas.",
          "La salida gira 21 veces más lenta que la entrada.",
          "El torque se divide por 21."
        ], correct:2,
        explain:"i>1 reduce velocidad e incrementa torque (idealmente)."
      },
      {topic:"7) Engranajes / relación i", q:"28. Si reduces rpm, ¿qué ocurre con el torque a la salida idealmente?",
        options:[
          "Disminuye necesariamente.",
          "Solo depende del diámetro del eje.",
          "Aumenta proporcionalmente a la relación de reducción (menos pérdidas).",
          "Se vuelve independiente de la carga."
        ], correct:2,
        explain:"Con potencia casi constante, al bajar ω aumenta T."
      },
      {topic:"7) Engranajes / relación i", q:"29. ¿Por qué se usan 2 etapas para reducciones grandes?",
        options:[
          "Para repartir cargas/tamaños y evitar engranes extremos en una sola etapa.",
          "Porque una sola etapa nunca funciona.",
          "Porque elimina la necesidad de rodamientos.",
          "Porque la norma lo prohíbe siempre."
        ], correct:0,
        explain:"Dos etapas permiten engranes razonables y menos esfuerzos."
      },
      {topic:"7) Engranajes / relación i", q:"30. ¿Qué consecuencias tiene una relación de transmisión mal calculada en una cinta transportadora?",
        options:[
          "No cumple velocidad/torque, puede sobrecargar, patinar o fallar por calentamiento.",
          "No tiene ninguna consecuencia.",
          "Solo cambia el color del tambor.",
          "Solo afecta el PLC, no lo mecánico."
        ], correct:0,
        explain:"i define rpm/torque: si está mal, falla funcional o se sobrecarga."
      },

      // 8) Rodamientos
      {topic:"8) Rodamientos (L10)", q:"31. ¿Qué es L10 y qué significa “90% de confiabilidad”?",
        options:[
          "Vida garantizada para 100%.",
          "Vida a la que 90% sobrevive y 10% falla bajo condiciones especificadas.",
          "La longitud del eje en mm.",
          "La carga estática del rodamiento."
        ], correct:1,
        explain:"Es una vida estadística con confiabilidad 90%."
      },
      {topic:"8) Rodamientos (L10)", q:"32. ¿Por qué se usa carga equivalente P si hay cargas combinadas?",
        options:[
          "Porque P es siempre igual a C.",
          "Para representar un caso equivalente que produce el mismo daño que las cargas reales combinadas.",
          "Para evitar calcular fuerzas.",
          "Para aumentar artificialmente la vida."
        ], correct:1,
        explain:"P combina cargas radial/axial en una carga equivalente para cálculo de vida."
      },
      {topic:"8) Rodamientos (L10)", q:"33. ¿Qué puede hacer que una vida teórica enorme no se cumpla en operación real?",
        options:[
          "Usar un catálogo en PDF.",
          "Lubricación deficiente, contaminación, desalineación, montaje, golpes, temperatura.",
          "Que la potencia esté en kW.",
          "Tener el eje pintado."
        ], correct:1,
        explain:"Factores de campo dominan la falla real."
      },
      {topic:"8) Rodamientos (L10)", q:"34. ¿Cómo afecta desalineamiento y mala lubricación a la vida del rodamiento?",
        options:[
          "Solo afecta el ruido, no la vida.",
          "La reduce drásticamente por aumento de carga local y fricción/calor.",
          "No afecta la vida.",
          "La aumenta porque “se acomoda”."
        ], correct:1,
        explain:"Genera cargas localizadas, calor y desgaste → falla prematura."
      },

      // 9) Fricción y contacto
      {topic:"9) Fricción y contacto", q:"35. En un freno de disco, ¿qué variables aumentan el torque de frenado?",
        options:[
          "Reducir Rm para aumentar torque.",
          "Aumentar μ, F normal o Rm (radio medio efectivo).",
          "Reducir μ para frenar más.",
          "Aumentar la rpm para frenar más."
        ], correct:1,
        explain:"T = μ·F·Rm."
      },
      {topic:"9) Fricción y contacto", q:"36. ¿Por qué aparece Rm (radio medio) y qué pasa si cambias Di y Do?",
        options:[
          "Porque Rm es constante siempre.",
          "Porque el esfuerzo de fricción se distribuye en el anillo; Di/Do cambia el radio efectivo y el torque.",
          "Porque Rm depende del PLC.",
          "Porque solo importa el área, no el radio."
        ], correct:1,
        explain:"Cambiar geometría cambia el brazo efectivo de fricción (Rm) y el torque."
      },
      {topic:"9) Fricción y contacto", q:"37. En un gripper, ¿por qué Fs ≥ W/(2μ)? ¿Qué representa el “2”?",
        options:[
          "Porque μ vale 2 por norma.",
          "Dos mordazas comparten el peso: cada una aporta fricción.",
          "Porque la gravedad se duplica por seguridad.",
          "Porque el objeto pesa el doble en operación."
        ], correct:1,
        explain:"Dos contactos aportan fricción; se reparte el soporte del peso."
      },
      {topic:"9) Fricción y contacto", q:"38. ¿Qué riesgo hay si asumes un μ demasiado alto sin validarlo?",
        options:[
          "Que el objeto deslice o el freno no alcance el torque real requerido.",
          "Que desaparezca la presión de contacto.",
          "Que aumente automáticamente la potencia del motor.",
          "Que la vida L10 siempre suba."
        ], correct:0,
        explain:"μ sobredimensionado en el papel falla en campo (humedad, polvo, desgaste)."
      },
      {topic:"9) Fricción y contacto", q:"39. ¿Cómo se relacionan p = F/A y desgaste?",
        options:[
          "El desgaste no depende de p.",
          "Mayor p suele aumentar desgaste y riesgo térmico/daño superficial.",
          "Mayor p siempre reduce desgaste.",
          "p solo afecta rodamientos, no frenos."
        ], correct:1,
        explain:"Presión alta incrementa esfuerzos de contacto, temperatura y desgaste."
      },

      // 10) Térmica en frenado
      {topic:"10) Térmica en frenado", q:"40. ¿Qué energía se transforma en calor durante un frenado?",
        options:[
          "Relación de transmisión i.",
          "Energía cinética (y/o potencial) del sistema.",
          "Vida L10.",
          "Esfuerzo equivalente Von Mises."
        ], correct:1,
        explain:"La energía mecánica se disipa como calor por fricción."
      },
      {topic:"10) Térmica en frenado", q:"41. ¿Qué factores controlan la temperatura máxima alcanzada?",
        options:[
          "Solo el límite de fluencia Sy.",
          "Energía por frenada, tiempo, capacidad térmica, ventilación, área y materiales.",
          "Solo el color del disco.",
          "Solo la potencia del PLC."
        ], correct:1,
        explain:"Depende de energía y capacidad de disipación (convección/conducción)."
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
          "Es el coeficiente de fricción.",
          "Es la fracción de calor que absorbe un componente; el resto se reparte a otros/ambiente.",
          "Es la relación de transmisión.",
          "Es la vida L10."
        ], correct:1,
        explain:"El calor se reparte: disco/pastilla/aire; no todo lo absorbe un solo elemento."
      },

      // 11) CAE/FEA
      {topic:"11) CAE / FEA", q:"44. ¿Qué diferencia hay entre “dimensionar” con cálculos y “verificar” con FEA?",
        options:[
          "FEA solo sirve para renders.",
          "Cálculo define tamaños; FEA valida distribución, picos y deformaciones.",
          "FEA reemplaza normas y cálculos siempre.",
          "Dimensionar solo sirve para eólica."
        ], correct:1,
        explain:"FEA es verificación; el dimensionamiento inicial viene de teoría."
      },
      {topic:"11) CAE / FEA", q:"45. ¿Qué condiciones de borde mal puestas pueden falsear resultados de esfuerzo?",
        options:[
          "Elegir fuente de letra incorrecta.",
          "Empotramientos irreales, cargas mal aplicadas, contactos mal definidos.",
          "Usar demasiados decimales.",
          "Modelar en mm en lugar de m (si todo está consistente)."
        ], correct:1,
        explain:"BC y contactos dominan tensiones y rigidez del modelo."
      },
      {topic:"11) CAE / FEA", q:"46. ¿Cómo usarías FEA para detectar concentraciones de esfuerzo?",
        options:[
          "Revisar mapas de tensión y picos en cambios de sección, filetes, agujeros, uniones.",
          "Mirar solo el peso del modelo.",
          "No mallar: usar malla 1 elemento.",
          "Desactivar contactos para acelerar."
        ], correct:0,
        explain:"Las concentraciones aparecen en discontinuidades y contactos."
      },
      {topic:"11) CAE / FEA", q:"47. Si el desplazamiento es grande pero los esfuerzos son bajos, ¿qué puede estar pasando?",
        options:[
          "Que Von Mises sea inválido.",
          "Problema de rigidez/BC, material mal asignado o estructura flexible aunque no exceda Sy.",
          "Que la fricción sea negativa.",
          "Que la rpm sea cero."
        ], correct:1,
        explain:"Puede ser un problema funcional de rigidez aun con tensiones elásticas."
      },

      // 12) Eólica
      {topic:"12) Eólica (Cp/TSR)", q:"48. ¿Qué es Cp y qué significa físicamente?",
        options:[
          "Coeficiente de potencia: fracción de energía del viento convertida en potencia útil.",
          "Relación de transmisión de engranes.",
          "Ciclo de vida L10 del rodamiento.",
          "Coeficiente de presión de contacto del freno."
        ], correct:0,
        explain:"Cp mide eficiencia aerodinámica de conversión de energía del viento."
      },
      {topic:"12) Eólica (Cp/TSR)", q:"49. ¿Qué es TSR y por qué existe un TSR óptimo?",
        options:[
          "Relación velocidad punta / velocidad viento; hay óptimo por aerodinámica del rotor.",
          "Torque/área; hay óptimo por costo.",
          "Temperatura superficial; hay óptimo por pintura.",
          "Tensión equivalente; hay óptimo por norma."
        ], correct:0,
        explain:"Cada geometría maximiza Cp en un rango de TSR."
      },
      {topic:"12) Eólica (Cp/TSR)", q:"50. Si TSR real es muy bajo respecto al óptimo, ¿qué implica en potencia extraída?",
        options:[
          "Que el freno disipa menos calor.",
          "Menor potencia (opera lejos del punto eficiente).",
          "Potencia independiente del viento.",
          "Mayor potencia automáticamente."
        ], correct:1,
        explain:"Lejos del TSR óptimo, Cp cae y se extrae menos potencia."
      },
      {topic:"12) Eólica (Cp/TSR)", q:"51. ¿Qué variables geométricas cambian el desempeño de un Savonius?",
        options:[
          "Solo el color del rotor.",
          "Radio, solape, forma/número de palas, altura y proporciones.",
          "Solo el tipo de rodamiento.",
          "Solo el PLC del sistema."
        ], correct:1,
        explain:"La geometría define arrastre/retorno y desempeño (Cp/TSR)."
      },

      // 13) Automatización y seguridad
      {topic:"13) Automatización y seguridad", q:"52. ¿Qué es un enclavamiento y por qué se usa para evitar movimientos peligrosos?",
        options:[
          "Un tornillo más grande para aguantar carga.",
          "Bloqueo lógico/eléctrico que impide acciones incompatibles (p.ej. invertir a la vez).",
          "Un lubricante especial.",
          "Una simulación de Von Mises."
        ], correct:1,
        explain:"Interlocks evitan comandos simultáneos o secuencias inseguras."
      },
      {topic:"13) Automatización y seguridad", q:"53. ¿Por qué los finales de carrera son críticos en una grúa?",
        options:[
          "Porque reemplazan los frenos.",
          "Evitan sobre-recorridos, choques y daños estructurales por exceder límites.",
          "Solo sirven para estética del tablero.",
          "Solo para aumentar rpm."
        ], correct:1,
        explain:"Detienen el movimiento en extremos para prevenir colisiones y sobrecarga."
      },
      {topic:"13) Automatización y seguridad", q:"54. ¿Qué diferencia hay entre seguridad estructural y seguridad operativa?",
        options:[
          "No hay diferencia.",
          "Estructural: no colapsa; operativa: control evita accidentes por maniobras/errores.",
          "Estructural: PLC; operativa: material.",
          "Estructural: rodamientos; operativa: engranes."
        ], correct:1,
        explain:"La estructura puede resistir, pero sin control y protecciones la operación puede ser peligrosa."
      },
      {topic:"13) Automatización y seguridad", q:"55. ¿Qué puede pasar si automatizas sin protección contra sobrecarga?",
        options:[
          "Se multiplica la potencia sin límites.",
          "Falla mecánica/eléctrica, daño por exceder capacidad y riesgo de accidente.",
          "Desaparece el calentamiento del freno.",
          "Mejora automática de la vida L10."
        ], correct:1,
        explain:"Sin protección, el sistema puede forzar cargas fuera de diseño."
      },
    ];

    // ====== Estado ======
    let quiz = [];
    let i = 0;
    let answers = [];
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
      quiz = clone(baseQuiz);
      if(shuffleMode.checked){
        shuffleArray(quiz);
        quiz.forEach(item=>{
          const zipped = item.options.map((t, idx)=>({t, idx}));
          shuffleArray(zipped);
          item.options = zipped.map(z=>z.t);
          item.correct = zipped.findIndex(z=>z.idx === item.correct);
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
      if(examMode.checked){ feedback.style.display = "none"; return; }
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

      if(answers[i]) applyAnswerState();
      else feedback.style.display="none";

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
      } else showResults();
    }

    function back(){
      if(i > 0){ i--; render(); }
    }

    function reset(){ buildQuiz(); }

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
      examMode.checked = false; // para ver explicaciones
      i = idxBad;
      render();
      if(answers[i]) applyAnswerState();
    }

    // Atajos 1..4
    window.addEventListener("keydown", (e) => {
      if(resultBox.style.display === "block") return;
      if(["1","2","3","4"].includes(e.key)) pick(parseInt(e.key,10)-1);
    });

    // Botones / modos
    btnNext.addEventListener("click", next);
    btnBack.addEventListener("click", back);
    btnReset.addEventListener("click", reset);
    btnReveal.addEventListener("click", () => {
      if(!answers[i]) return;
      if(examMode.checked){
        alert("Modo examen activado: las explicaciones se ven al final. Desactívalo para feedback inmediato.");
        return;
      }
      showFeedback(answers[i]);
      feedback.scrollIntoView({behavior:"smooth", block:"nearest"});
    });
    btnReview.addEventListener("click", reviewErrors);
    btnRestart2.addEventListener("click", reset);

    examMode.addEventListener("change", () => { if(answers[i]) applyAnswerState(); else render(); });
    shuffleMode.addEventListener("change", () => buildQuiz());

    // Init
    buildQuiz();
  </script>
</body>
</html>
