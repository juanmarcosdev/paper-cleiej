# Resumen técnico de cambios — CLEI EJ: *Cognitive Biases in Spiral-of-Silence Opinion Models*

**Fecha:** 2026-10-02
**Alcance:** revisión de redacción, estructura y presentación. **No se agregaron resultados, experimentos ni datos.** Ningún número de los experimentos cambió. Las pruebas conservan su contenido matemático; solo cambió la notación.
**Compilación:** `pdflatex → bibtex → pdflatex ×2` sin errores ni advertencias. El documento pasa de **20 a 21 páginas**. El abstract queda en **≈197 palabras** (límite de CLEI: 200).
**PDF de comparación:** `recursos/pdf/main_original.pdf` y `recursos/pdf/main_revisado.pdf`. Las páginas de este documento se indican como **orig. → nueva**.

## Fuentes y abreviaturas

| Clave | Fuente | Qué se tomó |
|---|---|---|
| **REF** | Aranda, Betancourt, Díaz, Paz, Valencia, *Fairness and Consensus in an Asynchronous Opinion Model for Social Networks* (JLAMP) | Estructura del abstract y de la introducción; explicación intuitiva tras cada definición; ejemplo resuelto; hoja de ruta de la prueba por etapas; sección única "Conclusions and Related Work" con diferencias explícitas frente a trabajos previos; pruebas esbozadas en el texto y completas en el apéndice; enlace al código desde la introducción. |
| **H§n** | Halmos, *How to Write Mathematics*, sección *n* | §5 organizar en torno a ejemplos; §6/§16 notación (sin choques de símbolos ni símbolos irrelevantes); §10 honestidad sobre el estatus de cada afirmación; §11 enunciar el teorema primero y sin irrelevancias; §14 "any" → "every/each"; §17 no empezar oraciones con un símbolo. |
| **M** | Milner, *Elements of Interaction* (Turing Lecture) | Visualizar con un caso concreto; aclarar con honestidad qué cubre el modelo y qué no ("many levels of explanation"). |
| **SN** | Springer Nature, *Writing in English* (lecciones completas en `recursos/springer/writing-in-english-springer.md`) | Una idea por oración (20–25 palabras como máximo); sujeto y verbo juntos; *topic/stress position*; comparaciones ("lower than", no "reduces compared to"); uso correcto de "respectively"; ortografía US consistente. |
| **NAT** | Diapositivas editoriales de Nature (`recursos/springer/nature-source-transcription.md`) | "Think of the reader", "No hype", contexto claro. |

## Archivos modificados (subir a Overleaf reemplazando los existentes)

| Archivo | Tipo de cambio |
|---|---|
| `main.tex` | Abstract reescrito; nuevo entorno `example` |
| `sections/introduction.tex` | Reestructurada siguiendo REF |
| `sections/model.tex` | Explicaciones intuitivas + **Ejemplo 1** nuevo |
| `sections/analysis.tex` | Hoja de ruta de la prueba; notación; leyendas; redacción |
| `sections/experiments.tex` | Redacción (oraciones cortas, comparaciones, menos adjetivos) |
| `sections/conclusions.tex` | Reestructurada siguiendo REF (sin subsecciones) |
| `appendix/proofs.tex`, `appendix/proof_cbsom_bounds.tex`, `appendix/proof_consensus_n3.tex`, `appendix/proof_geom_decay.tex` | Notación $R_t\to\Delta_t$; ortografía; cuantificadores |

| `references.bib` | Nueva entrada `gaona2024opinion` |

**Sin cambios:** `macros.tex`, `cleiej.cls`, `IEEEtran.bst`, `figs/*`.

---

## 1. Abstract (`main.tex`) — pág. 1 → 1

- **Qué:** se reescribió completo con la secuencia de REF: (1) qué modelo se introduce, (2) cómo funciona un paso, en lenguaje llano, (3) qué se prueba, (4) qué muestran las simulaciones.
- **Cómo:** se agregó la descripción operativa ("every agent passes its disagreement with each influencer through a bias function… It then decides whether to speak or to remain silent"). También se explicita qué diferencia a CBSOM⁻ de CBSOM⁺ (los silenciosos no influyen frente a influir con su última opinión pública).
- **Eliminado:** detalles de implementación ("high-performance Scala/Akka actor-based simulator… bias-aware persistence layer") y la frase final de impacto ("implications for… polarization-mitigation strategies"). [NAT: no hype; REF no incluye detalles de implementación en el abstract]
- **Ajuste de precisión:** "backfire and authority biases robustly preclude agreement" pasa a "almost always prevent it", porque Authority muestra eventos aislados en n = 10 (Sec. 4.2). [H§10]
- **Extensión:** 197 palabras.

## 2. Introducción (`sections/introduction.tex`) — págs. 1–2 → 1–2

| Párrafo | Cambio | Guía |
|---|---|---|
| P1 "Social networks have a strong impact…" | Reemplaza "The rise of digital social platforms…". Abre como REF, con oraciones más cortas. | REF, SN |
| P2 DeGroot | "repetitively" → "repeatedly". La frase redundante "consensus is a central indicator of a non-polarized community; indeed, the inability…" se cambia por la formulación de REF ("consensus is a central problem in social learning. Indeed, …"). | REF, H§9 |
| P3 dos supuestos | Ahora inicia con "Nevertheless, the DeGroot model makes two assumptions…" (como REF). | REF |
| P4 Spiral of Silence | Una oración de 37 palabras se divide en tres. Se mantiene "That work is the direct predecessor of the present paper." | SN (una idea por oración) |
| P5 sesgos + Alvim | Los párrafos de sesgos y de Alvim et al. se fusionan. Se eliminan las negritas "**The central contribution of the present paper is to unify both dimensions**". | NAT (no hype) |
| **P6 nuevo** "In this paper, we combine both phenomena…" | Descripción intuitiva del modelo: el estado tiene opinión y vocal/silencioso; en cada paso se revisa la opinión pasando el desacuerdo por el sesgo y luego se decide si hablar según el radio de tolerancia. Se aclara que **los silenciosos siguen actualizando su opinión**. Diferencia entre CBSOM⁻ y CBSOM⁺. | REF (párrafo análogo "In this paper, we introduce… OTS") |
| **P7 nuevo** "We focus on the problem of convergence to consensus…" | Narrativa de resultados en orden: (1) propiedades estructurales preservadas bajo sesgos en R; (2) consenso en cliques para F_α, incluido n = 2; (3) qué cubren las simulaciones que la teoría no cubre. | REF, M |
| **P8 nuevo** "To the best of our knowledge…" | La afirmación de novedad, que antes solo estaba en Conclusiones, se adelanta. | REF |
| Contributions | Ítem 2: "specifically, …—" pasa a "namely, …". Ítem 3: sin cambio de contenido. **Ítem 4 cambia:** antes "(iii) network size and topology interact with bias type in nuanced ways not predicted by small-scale analyses" (vago). Ahora lista los hallazgos de la Discusión 4.5: (iii) umbral sub-lineal y (iv) memoria. | H§3 (decir algo concreto) |
| Organization | Se agrega, como REF: "For the sake of readability, some proofs are only outlined in the main text; the complete proofs are given in Appendix A." y el **enlace al simulador en GitHub** (que antes solo aparecía al final de la Sec. 4). | REF |

## 3. Modelos (`sections/model.tex`) — págs. 2–6 → 2–6

| Ubicación (nueva pág.) | Cambio | Guía |
|---|---|---|
| Tras **Definición 1** (p. 3) | **Párrafo nuevo** que explica cada componente: vértices = agentes; (j,i) ∈ E = j influye en i; I(j,i) = fuerza; Ec. (1) = los pesos suman 1. | REF ("The vertices in A represent…") |
| Párrafo de opiniones (p. 3) | Se agrega: "If $B_i^t=0$, agent i completely disagrees…; if $B_i^t=1$, it completely agrees". | REF |
| Tras **Definición 2** (p. 3) | Nueva frase intuitiva: "β_{i,j}(x) is the part of the disagreement x that agent i actually absorbs…; the identity corresponds to DeGroot". | REF, H§8 |
| Párrafo del *clamp* (p. 3) | Antes decía "Throughout this paper all bias functions lie in R", lo cual es falso porque las Secs. 4.x usan Backfire/Authority. Ahora dice "**Our formal results** assume bias functions in R". | H§10 (honestidad sobre el alcance) |
| Regiones de sesgo (p. 3–4) | "region of $S=[-1,1]^2$" → "region of the square $[-1,1]^2$". La letra $S$ ya denota el vector de silencio. | H§6, H§16 |
| "The R-region is central…" (p. 4) | Se explica *por qué*: "A bias in R moves an agent towards each influencer, but never beyond it." | M, H§10 |
| Tras Ecs. (4)–(5), SOM⁻ (p. 4) | Nueva oración: "Silent agents still revise their own opinions through (4); they only stop expressing them." | H§4 (anticipar dudas del lector) |
| SOM⁺ y CBSOM⁺ (p. 4–5) | Las oraciones que empezaban con un símbolo ("\SOMplus is…", "\CBSOMplus applies…") pasan a "the model SOM⁺ is…", "The model CBSOM⁺ applies…". La frase "temporal-cognitive coupling" se reescribe en lenguaje llano. | H§17 |
| Lema 2 / Corolario 3 (p. 5) | "For any / In any" → "For every / In every". | H§14 |
| **Ejemplo 1 nuevo** (p. 5, tras la explicación de la Def. 5) | Clique de 3 agentes, $I_{ji}=1/2$, $\mathbf B^0=(1,0.5,0)$, $\tau_i=0.4$, sesgo $\beta(x)=x/2$. Se calcula $B_1^1=0.625$ y $\mathbf B^1=(0.625,0.5,0.375)$; sin sesgo daría $(0.25,0.5,0.75)$ (los agentes 1 y 3 se cruzan). Luego todos callan ($\mathbf S^1=\mathbf 0$), $\mathbf B^2=\mathbf B^1$, todos vuelven a hablar ($\mathbf S^2=\mathbf 1$) y convergen a 0.5. Así se anticipa el Lema 5. **Los valores se verificaron numéricamente con las Ecs. (8)–(9).** Usa los mismos parámetros de las Figs. 2–3, salvo $\tau_i$. | REF (Example 1), H§5 ("organize around the central examples"), H§8 (pista que anticipa un resultado posterior), M |
| Sec. 2.6 (p. 6) | "DeGroot is…" → "The DeGroot model is…"; "Any result…" → "Therefore, every result…". | H§14, H§17 |
| `main.tex` | Nuevo `\newtheorem{example}{Example}` (estilo *definition*) para el ejemplo. | — |

## 4. Análisis (`sections/analysis.tex`) — págs. 5–10 → 6–10

| Ubicación (nueva pág.) | Cambio | Guía |
|---|---|---|
| Apertura de la Sec. 3 (p. 6) | **Hoja de ruta nueva** en tres etapas numeradas: (1) silencio y sesgo no interfieren y los extremos convergen a U, L; (2) F_α contrae la dispersión en cliques; (3) contradicción ⇒ U = L, y el caso n = 2 aparte. Antes de las etapas se enuncian los teoremas principales (12 y 14). | REF (Sec. 5: "we outline its proof by dividing it in three stages"), H§11 (teorema primero) |
| Sec. 3.1, primer párrafo (p. 6) | "We show that the answer is affirmative: … —not on…— so…" se divide en tres oraciones. | SN |
| Lema 5 y prueba (p. 6) | "For any" → "For every"; "Note that this argument is independent of…" → "The argument does not use the bias functions". | H§14, SN (concisión) |
| Entre el Cor. 6 y el Lema 7 (p. 6) | Frase intuitiva nueva: "silence can block every channel of influence for one round, but not for two consecutive rounds… no agent can move beyond the current extreme opinions." | REF ("Intuitively, …") |
| Esbozo del Lema 7 (p. 6) | Oraciones separadas; "toward" → "towards"; "Full proof in Appendix A." → "The full proof is in Appendix A." | SN |
| Prueba del Teo. 9 (p. 7) | Empezaba con el símbolo "$\{\max(\mathbf B^t)\}$ is…"; ahora "The sequence … is…". | H§17 |
| **Notación de la dispersión** (p. 7 y apéndice) | $R_t$ → **$\Delta_t$** en todo el texto y el apéndice. $R$ ya es la región *Receptive-Resistant*, y frases como "Since β ∈ R… R_t < ε" eran ambiguas. Además $\Delta_t\to\delta=U-L$ concuerda con la $\delta$ que ya usa la prueba del Teo. 12. | H§6 ("think about the alphabet"), H§16 |
| Fig. 1, leyenda y texto (p. 7) | "on the domain $S=[-1,1]^2$" → "on the square $[-1,1]^2$". | H§6 |
| Enunciado del **Lema 11** (p. 7) | Se quitan $\alpha_{\min}$ e $I_{\min}$ del enunciado (no se usan allí). Ahora se definen al inicio del esbozo de prueba, que es donde se usan. El esbozo se reescribe en oraciones cortas. | H§16 ("avoid irrelevant symbols"), H§11 |
| Esbozo del Teo. 12 (p. 8) | ": contradiction." → ", a contradiction."; "Full proof in…" → "The full proof is in…". | SN |
| Leyenda de la Fig. 3 (p. 8) | "f_α converges faster than conf(x) due to stronger linear attenuation of disagreement at all scales" → "Consensus is reached faster than under conf(x), because f_α attenuates disagreements of every size linearly". Se compara lo comparable: consenso con consenso. | SN (*Comparisons*: comparar cosas equivalentes) |
| Sec. 3.3.2, primer párrafo (p. 8) | "The SOM⁻ model fails to converge on two-agent cliques" → "**can fail** to converge". La oscilación ocurre para ciertos parámetros, no siempre. | H§10 |
| Remark 3.3, "Recovery of the n = 2 pathology" (p. 9) | "larger α produces oscillatory… smaller α yields monotone…" se precisa: "**If 2αI > 1**, then γ < 0 and the dynamics oscillate but still converge; **if 2αI < 1**, then γ > 0 and convergence is monotone." Es consistente con las Figs. 5 (α = 0.1) y 6 (α = 0.9) y con el caso α = 0.5 ⇒ γ = 0. | H§10, H§15 (precisión) |
| Texto antes de la Fig. 5 y leyenda de la Fig. 5 (p. 9) | **Referencia rota eliminada:** "Case 2 of Theorem 14" pasa a "Theorem 14". El Teorema 14 no tiene casos (es un remanente de la tesis). | H§10 |
| Leyendas de las Figs. 5–6 (p. 9) | Comas tras cláusulas introductorias; la oración larga de la Fig. 6 se divide en dos. | SN |
| Sec. 3.4, último párrafo (p. 10) | Las rayas "—formalized in Lemma 5—" pasan a comas. | SN |

## 5. Evaluación experimental (`sections/experiments.tex`) — págs. 10–16 → 10–16

**Todos los valores numéricos, tamaños, densidades y conteos de corridas se mantienen idénticos.**

| Ubicación (nueva pág.) | Cambio | Guía |
|---|---|---|
| Apertura de la Sec. 4 (p. 10) | "We corroborate the theoretical results…" → se explica que las simulaciones estudian **lo que la teoría no cubre** (grafos libres de escala, sesgos fuera de R, mezclas, memoria). "(i) to confirm empirically that only R-region…" → "to **test** whether only…". | M ("many levels of explanation"), H§10 |
| Configuración de la simulación (p. 11) | La oración del exponente γ = 2.5 se divide en dos. | SN |
| **Metrics** (p. 11) | `\noindent\textbf{}` → `\paragraph{}`, para que todos los encabezados de párrafo sean consistentes. "average round count" → "average number of rounds". | H§15 (consistencia) |
| Sec. 4.2, memoryless (p. 11) | Oraciones divididas. "CBSOM⁻ (Conf.) achieves 70% versus 10% for SOM⁻" → "the consensus rate is 70% for … and 10% for …". "uniformly black (zero consensus at every scale and density)" → "uniformly black, i.e., there is no consensus at any scale or density". | SN (*Comparisons*, concisión) |
| Párrafo del umbral sub-lineal (p. 11) | Una oración de 50+ palabras se divide en cuatro. El paréntesis "(in all observed runs for n ≤ 10⁵, where run counts are 50 or greater)" pasa a una oración propia. | SN |
| Sec. 4.2, memory-based (p. 11) | "contrasts sharply with" → "differs markedly from"; "achieves a single consensus run under any density" → "reaches consensus in a single run at any density"; "dissolves entirely" → "disappears". | NAT, SN |
| Sec. 4.3, introducción (p. 13) | Se reformula la lista de configuraciones. | SN |
| **Rationale for the choice of proportions** (p. 13) | Un párrafo de ≈350 palabras se divide en **3 párrafos**: (a) por qué son heurísticas, (b) qué pregunta responde cada configuración, (c) gradiente y trabajo futuro. Cada oración larga se divide. El contenido no cambia. | SN, H§17 (aspecto de la página) |
| **Configuración (i), memoryless** (p. 13) | **Corrección de consistencia interna:** el texto decía "Configuration (i)—an R-region majority" y "a 70% R-region fraction… even when 30% of edges carry no bias". La propia lista de la sección define (i) como **SOM⁻ 70% / CBSOM⁻(Conf.) 30%**, es decir, 30% de confirmación y 70% sin sesgo. Ahora dice: "mixing confirmation-biased and unbiased edges in a 30/70 proportion preserves the robustness of consensus". **Por favor confirmar.** | H§10 |
| Configuraciones (ii)–(iv) (p. 14) | Se elimina "Remarkably, a mere…". "consensus killers" → "prevent consensus". "with probability approaching 100%" → "in almost every run". | NAT (no hype) |
| Memory-based no uniforme (p. 14) | "Memory thus amplifies… to a **structural impossibility** at scale" → "…at scale, **we observed no consensus at all**". Una simulación no demuestra imposibilidad. | H§10 |
| Leyenda de la Fig. 10 (p. 14) | "any fraction of" → "Every configuration that contains…"; "sharp robustness asymmetry" → "robustness asymmetry". | H§14, NAT |
| Sec. 4.4, introducción (p. 14) | Oraciones divididas; "parameterize" → "measure". | SN |
| **Encabezados Row 1–4** (p. 14–15) | "Row 1/2/3/4" no correspondía a la numeración de las figuras, que tienen 2 filas cada una. Ahora: "Uniform memoryless (**Figure 11, top row**)", "(Figure 11, bottom row)", "(Figure 12, top row)", "(Figure 12, bottom row)". | H§4 (anticipar confusión del lector) |
| Uniform memoryless (p. 14) | "confirm that the bias-region dichotomy is a property of the bias type alone, independent of connectivity level" → "indicate that, **in this range**, the dichotomy depends on the bias type alone…". | H§10 |
| Cierre de la Sec. 4.4 (p. 15) | "Together, Rows 2 and 4 sharpen…" → "Together, the two memory-based scenarios sharpen…", dividido en oraciones. | SN |
| Leyenda de la Fig. 11 (p. 15) | "--- the bias dichotomy is fully density-invariant" → "; the bias dichotomy does not depend on density". | SN |
| Discusión 4.5, ítem 1 (p. 16) | "Sharp bias-region dichotomy" → "Bias-region dichotomy"; el paréntesis "(run counts ≥ 50)" pasa a texto. | NAT |
| **Discusión 4.5, ítem 2** (p. 16) | "Confirmation consistently **reduces** the threshold by one unit **compared to** the unbiased SOM⁻ baseline" → "The threshold under Confirmation is consistently one unit **lower than** under the unbiased SOM⁻ baseline". | SN (*Comparisons* regla 3: "reduced" solo compara contra un estado anterior) |
| Discusión 4.5, ítem 3 (p. 16) | Oraciones divididas; "memory-induced path dependence" → "the path dependence induced by memory". | SN |

## 6. Conclusiones (`sections/conclusions.tex`) — págs. 16 → 16–17

- **Estructura:** antes eran 5.1 *Conclusions* (resumen + trabajo futuro) y 5.2 *Related Work*. Ahora es **una sola sección sin subsecciones**, en el orden de REF: **resumen → trabajo relacionado → trabajo futuro**.
- **Párrafo 1 (resumen):** se precisa que las propiedades estructurales se probaron para el **modelo memoryless**. Las simulaciones se describen como complemento ("complement these results"), no como confirmación de la teoría en dominios que la teoría no cubre. Se conserva "To our knowledge, this is the first work…". [H§10]
- **Párrafo 2 (Alvim et al.):** empieza con "The work closest to ours is…" y declara la diferencia explícita "Unlike [17], our consensus result is restricted to cliques and to F_α", como hace REF con Fagnani. Se eliminó la frase "Extending it to all continuous R-biases on arbitrary strongly connected graphs remains an open problem." [REF]
- **Párrafo 3 (Aranda et al.):** mismo contenido. "this mirrors the behavior… and **confirms** that memory acts as a structural barrier" → "and **suggests** that memory acts as a barrier", porque la evidencia es empírica. [H§10]
- **Párrafo 4 NUEVO (otros trabajos relacionados):**
  - Modelos de confianza acotada (**Deffuant et al. 2000**, nueva cita; la entrada ya estaba en `references.bib` pero no se citaba). Diferencia: en estos modelos el umbral decide *a quién se escucha*, mientras que el $\tau_i$ de este paper decide *si se habla*.
  - Simulaciones agente-base de la espiral del silencio (Sohn 2022, Wang 2013, Ross 2019, Cabrera 2021, ya citadas en la introducción): el paper "follows this line, and complements it with formal results for the clique case". [REF: ubicar el trabajo frente a la literatura]
- **Párrafo 5 (trabajo futuro), reducido a dos puntos:** (1) extender los sesgos cognitivos a los modelos de silencio basados en confianza de **Gaona** (nueva cita `gaona2024opinion`, tesis de maestría, Univalle 2024, agregada a `references.bib`); (2) topologías de red dinámicas. Se eliminaron la extensión del análisis a grafos fuertemente conexos arbitrarios, la contraparte formal para CBSOM⁺ y el acoplamiento con datos empíricos.

## 7. Apéndice — págs. 18–20 → 18–21

| Archivo | Cambio |
|---|---|
| `appendix/proofs.tex` | "In this appendix, the reader may find the complete proofs…" → "This appendix contains the complete proofs…" [SN: concisión] |
| `appendix/proof_cbsom_bounds.tex` | "Fix any agent" → "Fix an agent" [H§14]; "We **analyse**" → "We **analyze**" (ortografía US consistente con el resto) [SN: *Spelling*]; "of $S=[-1,1]^2$" → "of the square $[-1,1]^2$" [H§6] |
| `appendix/proof_geom_decay.tex` | $R_t\to\Delta_t$ (23 ocurrencias); "For any ε" → "For every ε" [H§6, H§14] |
| `appendix/proof_consensus_n3.tex` | $R_t\to\Delta_t$ (7 ocurrencias) [H§6] |

## 8. Lo que NO se cambió (decisiones deliberadas)

- **Título:** se mantiene. Si los profesores quieren acercarlo al estilo de REF (*Fairness and Consensus in an Asynchronous Opinion Model for Social Networks*), una opción es *Cognitive Biases and Consensus in Spiral-of-Silence Opinion Models for Social Networks*.
- **Resultados, figuras, tablas y datos:** sin cambios.
- **Contenido matemático de las pruebas:** sin cambios. Solo cambió la notación ($\Delta_t$) y la redacción.
- **"Highlights" e índice de símbolos de REF:** no se agregaron. Son requisitos de Elsevier/JLAMP y no de CLEI EJ.
