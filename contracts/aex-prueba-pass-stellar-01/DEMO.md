# Demo en video (3 min)

Entregable de Stellar Elite Bolivia: invocación exitosa desde el Stellar CLI, el evento y el estado resultante en el explorer, y qué sigue.

## Antes de grabar

Ya está hecho: contrato desplegado en testnet con el alias `aex-prueba-pass-stellar-01`, e identidades `anfitrion` y `asistente` creadas y fondeadas con Friendbot.

- Abre una terminal en la raíz de `Stellar-Build` y hazla grande (fuente ≥ 18).
- Deja abiertas en el navegador:
  - el contrato: https://stellar.expert/explorer/testnet/contract/CCGIRQW6WUR4WT46DTL2EZMQBCY4SNRF622DN2VODMOYGMSFHMDPP6NW
  - `contracts/aex-prueba-pass-stellar-01/src/lib.rs` en el editor.
- Cada comando se ejecuta **una sola vez**: `buy` y el primer `check_in` cambian el estado para siempre. Si quieres ensayar, hazlo con otra identidad (`stellar keys generate ensayo --network testnet --fund`) y cambia `asistente` por `ensayo`.

## Comandos

```bash
stellar contract invoke --id aex-prueba-pass-stellar-01 --source-account anfitrion --network testnet -- name
```

```bash
stellar contract invoke --id aex-prueba-pass-stellar-01 --source-account asistente --network testnet -- pass_of --buyer asistente
```

```bash
stellar contract invoke --id aex-prueba-pass-stellar-01 --source-account asistente --network testnet -- buy --buyer asistente
```

```bash
stellar contract invoke --id aex-prueba-pass-stellar-01 --source-account anfitrion --network testnet -- check_in --buyer asistente
```

```bash
stellar contract invoke --id aex-prueba-pass-stellar-01 --source-account anfitrion --network testnet -- check_in --buyer asistente
```

```bash
stellar contract invoke --id aex-prueba-pass-stellar-01 --source-account asistente --network testnet -- pass_of --buyer asistente
```

Resultados esperados, en orden: `"Aex Prueba Pass Stellar 01"` · `null` · éxito con link a stellar.expert · éxito con link · **`Error(Contract, #4)`** (`AlreadyUsed`) · `"Used"`.

## Guion

**0:00–0:25 · Presentación**
> Soy Alejandro Montecinos, de Stellar Elite Bolivia. Estoy construyendo Pollar Pass, un sistema de entradas sobre Stellar. Para este entregable llevé su regla central a un contrato Soroban, en el track Event Pass: **Aex Prueba Pass Stellar 01**, un pase para entrar a un Meet.

**0:25–0:55 · El contrato** (en pantalla: `lib.rs`)
> Tiene dos funciones clave. `buy`: el asistente firma, paga 1 XLM al anfitrión y queda registrado con su pase. `check_in`: solo el anfitrión la firma, cuando admite a la persona en el Meet, y el pase pasa de comprado a usado. El link del Meet no está en el contrato, porque todo lo on-chain es público: el contrato solo prueba quién pagó y quién entró.

**0:55–1:50 · Invocación** (terminal, comandos en orden)
> Este es el evento. El asistente todavía no tiene pase. Compra: paga y el contrato lo registra. En la puerta del Meet, el anfitrión hace check-in: éxito. Si alguien intenta entrar otra vez con el mismo pase, el contrato lo rechaza: error 4, AlreadyUsed. Esa es la garantía: el ledger no deja usar un pase dos veces, ni siquiera al anfitrión.

**1:50–2:25 · Explorer** (stellar.expert)
> En la transacción del `buy` se ve la transferencia de 1 XLM al anfitrión y el evento `bought`. En la del `check_in`, el evento `checked_in` con la address del asistente. Y en el storage del contrato, el pase de esta address queda en `Used`. Todo público y verificable.

**2:25–3:00 · Qué sigo aprendiendo**
> Lo siguiente es conectar este contrato a Pollar Pass, para que la puerta verifique los pases directamente en el ledger. Para eso tengo que profundizar en tres cosas: el TTL y la renta del storage, para que los pases no expiren antes del evento; tests más completos, como fuzzing, antes de mover dinero real; e invocar contratos desde el frontend con la wallet del usuario, sin CLI.
