# Stellar Build

Repositorio base de mi proyecto para **Stellar Elite Bolivia**.

Viene del template oficial [`salazarsebas/stellar-build-toolkit`](https://github.com/salazarsebas/stellar-build-toolkit), generado desde [stellarbuild.acachete.xyz](https://stellarbuild.acachete.xyz). Todavía no hay código de aplicación: por ahora esto es el **toolkit de skills** con el que voy a construir durante el programa.

## Qué hay acá

`.claude/skills/` — 34 skills para Claude Code, más `SKILL_ROUTER.md` que decide cuál usar en cada momento.

### Stellar y Soroban

| Skill | Para qué |
|---|---|
| `smart-contracts` | Contratos en Rust con `soroban-sdk`: setup, desarrollo y pruebas |
| `dapp` | Frontend con el `stellar-sdk` de JavaScript, en navegador y Node |
| `assets` | Assets clásicos, trustlines y el puente SAC hacia contratos |
| `data` | Consultar datos de la cadena vía Stellar RPC y Horizon |
| `standards` | SEPs, CAPs y referencia del ecosistema |
| `deploy-stellar-mainnet` | Checklist de devnet → mainnet |
| `agentic-payments` | Pagos máquina a máquina y APIs pagas (x402) |
| `zk-proofs` | Pruebas de conocimiento cero y patrones de privacidad |
| `find-stellar-idea` | Descubrir qué construir sobre Stellar |
| `stellar-competitive-landscape` | Mapear competencia de una idea |
| `scf-round-watcher` | Seguir rondas del Stellar Community Fund |
| `stellar-help` | Orientación sobre qué skill usar según el estado del proyecto |

### Producto y proceso

`prd` · `product-brief` · `prfaq` · `create-epics-and-stories` · `create-architecture` · `create-ux-design` · `dev-story` · `brainstorming` · `advanced-elicitation` · `reprompt` · `investigate` · `bri-tech-writer` · `remove-ai-marks`

### Revisión

`code-review` — revisión adversarial en capas paralelas
`review-edge-case-hunter` — recorre ramas y condiciones límite buscando casos sin manejar

### Roles

`nicole-pm` · `justin-analyst` · `tyler-architect` · `elliot-dev` · `kaan-ux-designer` · `party-mode` (discusión entre varios) · `navigate-skills` (explorar todas)

## Cómo se usa

Las skills se activan solas en [Claude Code](https://claude.com/claude-code) según lo que pidas. Para ver el catálogo completo desde adentro del proyecto:

```
/navigate-skills
```

## Licencia

El contenido de `.claude/skills/` viene del template y pertenece a sus autores. El código de mi proyecto llevará su propia licencia cuando exista.

---

**Alejandro Tintaya Montecinos** — La Paz, Bolivia
[latmontecinos.vercel.app](https://latmontecinos.vercel.app)
