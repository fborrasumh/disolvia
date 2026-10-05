# DisolvIA

Misiones de Fisicoquímica (Grado en Farmacia) que se adaptan a tus fallos. Aplicación web de un solo fichero (`index.html`).

**Usar la app:** https://fborrasumh.github.io/disolvia/ *(cuando se publique)*

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23168927.svg)](https://doi.org/10.5281/zenodo.23168927)

**Idiomas:** español (por defecto), inglés y portugués; selector en la barra superior (o `?lang=en` / `?lang=pt` en la URL).

## Qué hace

- **22 misiones** en cuatro bloques, con dificultad progresiva y prerrequisitos recomendados:
  - *Preparar disoluciones* (9): unidades y prefijos · % m/V y m/m · molaridad (de los moles a la masa que se pesa y al matraz aforado) · sales hidratadas y pureza · molaridad de un reactivo comercial (% y densidad) · dilución desde el comercial · mezclas y diluciones seriadas · inyectables: % m/V → mmol → mEq · osmolaridad e isotonía.
  - *Propiedades coligativas y fases* (6): presión de vapor (Raoult) · crioscopia y ebulloscopia · masa molar por crioscopía · presión osmótica · diagrama de fases del agua y regla de las fases · reparto y extracción.
  - *Cinética química* (5): orden de reacción y leyes integradas · semivida y caducidad (t90) · obtener k de datos · Arrhenius y estabilidad acelerada · vías paralelas.
  - *Fenómenos de transporte* (2): difusión (Fick) · sedimentación (Stokes).
- **Cada ejercicio se genera con una semilla**: cada estudiante recibe números distintos y la misma semilla da siempre el mismo ejercicio (el profesorado puede reproducirlo).
- **El motor calcula; la IA no.** Todas las soluciones salen de código determinista. Se probó con 400 variantes por misión (más de un millón de comprobaciones) y con oráculos independientes que recalculan desde el propio enunciado.
- **Diagnóstico por recálculo.** Los fallos típicos (masa para un litro en vez de para el matraz, Mr del anhidro en vez del hidrato, olvidar el factor *i*, grados Celsius en lugar de kelvin, contar un paso de menos en una serie…) se declaran como variantes del cálculo; si la respuesta coincide con una, la app explica el fallo. También detecta «el número está bien, la unidad no», «esa cifra es la respuesta de otro paso» y factores típicos (×1000, ×60, ln/log, signo…).
- **Ejercicio de refuerzo relacionado.** Según el fallo, la app propone otra misión más básica; al terminarla se vuelve al ejercicio original.
- **Juego sin trampas:** estrellas (3 si no hay fallos ni pistas), puntos, niveles, racha y repaso espaciado (1, 3, 7 y 21 días; los fallos vuelven antes). Preguntas de comprensión («¿cómo se prepara de verdad?», «¿hipo, iso o hipertónica?») además de cálculos.
- **Informe para entregar** (Word, JSON, CSV) con misiones, aciertos y fallos más frecuentes, y un registro encadenado con huellas SHA-256.
- **Comprobación por el profesorado:** carga el JSON del estudiante, verifica la cadena y recalcula cada respuesta con su semilla.

## Cómo se usa la IA (opcional)

La app funciona entera sin clave. Con la propia clave de OpenAI, Google Gemini o Anthropic Claude, el botón «Explícamelo con otras palabras» pide una explicación del concepto que falla. La IA **no recibe la solución**; su respuesta se filtra por código y se eliminan las frases que contengan la cifra correcta (en cualquier potencia de 10) o el texto de la opción correcta. La clave se guarda solo en el navegador.

## Privacidad

El progreso, el informe y la clave se guardan en el navegador (IndexedDB / localStorage). Solo si se pide ayuda a la IA sale el enunciado del paso y la respuesta del estudiante (sin su nombre), y antes del primer envío se muestra exactamente lo que sale. No hay servidor.

## Límites

- Los ejercicios son **de elaboración propia** del motor; **no se reutilizan** los del libro de ejercicios resueltos de la profesora, que queda como referencia (en la guía docente: «Disoluciones. Aplicación a la preparación de inyectables», Varea, Crespo, Galindo y Yubero).
- Se supone comportamiento ideal (coeficiente *i* ideal, volúmenes aditivos en disoluciones diluidas); los valores de referencia (Kf, Kb, P° del agua, 300 mOsm/L para el plasma…) están dados en cada enunciado.
- El registro encadenado **detecta ediciones del fichero; no es una prueba definitiva** (quien sepa puede recalcular la cadena). Por eso el recálculo con semillas es la comprobación importante.
- La guía docente menciona también electroquímica y macromoléculas/coloides; no figuran en las unidades didácticas y no están incluidas.
- Las explicaciones de la IA pueden equivocarse; el cálculo lo hace siempre el motor.
- No se ha probado con una clave real de IA (solo con respuestas simuladas, incluidas respuestas que intentan revelar la solución).

## Autoría

Fernando Borrás Rocher (Universidad Miguel Hernández de Elche) y Montserrat Varea Morcillo (Universidad Miguel Hernández de Elche).

A partir de la idea de la profesora Montserrat Varea Morcillo (Fisicoquímica, Grado en Farmacia): un juego de ejercicios que se resuelven paso a paso y que, según el fallo, llevan a otro ejercicio relacionado, para que el alumnado entienda qué significa preparar una disolución.

ORCID: Fernando Borrás Rocher [0000-0002-5519-4573](https://orcid.org/0000-0002-5519-4573) · Montserrat Varea Morcillo [0000-0001-9153-4953](https://orcid.org/0000-0001-9153-4953)

## Cómo citar

Borrás Rocher, F. y Varea Morcillo, M. (2026). *DisolvIA* (v1.0.0) [Software]. DOI: [10.5281/zenodo.23168927](https://doi.org/10.5281/zenodo.23168927)

## Desarrollo y pruebas

```bash
python3 build.py                      # monta index.html desde src/ y forja/
node tests/logic_test.js              # motor: 22 misiones × 400 semillas + oráculos independientes
NODE_MODULES=/ruta/node_modules python3 tests/smoke_test.py   # navegador (Playwright), IA simulada, es/en/pt, móvil
```

## Licencia

MIT. Véase [LICENSE](LICENSE).
