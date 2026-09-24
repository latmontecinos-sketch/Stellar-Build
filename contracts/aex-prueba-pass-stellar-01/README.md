# Aex Prueba Pass Stellar 01

Contrato Soroban del track **Event Pass** de Stellar Elite Bolivia: un pase de acceso a un Meet. El ledger verifica dos cosas:

1. que una address **compró su pase**, pagando el precio al anfitrión, y
2. que ese pase **se usó una sola vez**.

El link del Meet no vive en el contrato. Todo lo que está on-chain es público, así que el anfitrión lo comparte fuera de la red; el contrato solo prueba quién pagó y quién entró.

## Funciones

| Función | Firma | Qué hace |
|---|---|---|
| `__constructor(host, token, price, name)` | al desplegar | Fija anfitrión, activo de pago, precio y nombre del evento. Rechaza precios ≤ 0 |
| `buy(buyer)` | el comprador | Transfiere `price` del comprador al anfitrión y guarda el pase como `Bought`. Una address compra un solo pase |
| `check_in(buyer)` | el anfitrión | Al admitir a la persona en el Meet, pasa el pase de `Bought` a `Used` y emite `checked_in` |
| `pass_of(buyer)` | nadie | Estado del pase: `null`, `Bought` o `Used` |
| `name()` · `price()` · `host()` | nadie | Configuración del evento |

**Eventos:** `bought` (topic: comprador · data: precio) y `checked_in` (topic: comprador).

**Errores:**

| Código | Error | Cuándo |
|---|---|---|
| `#1` | `InvalidPrice` | Precio ≤ 0 al desplegar |
| `#2` | `AlreadyBought` | La address ya tiene pase |
| `#3` | `NoPass` | Check-in de alguien que no compró |
| `#4` | `AlreadyUsed` | Segundo check-in con el mismo pase |

## Despliegue en testnet

| | |
|---|---|
| Contrato | [`CCGIRQW6WUR4WT46DTL2EZMQBCY4SNRF622DN2VODMOYGMSFHMDPP6NW`](https://stellar.expert/explorer/testnet/contract/CCGIRQW6WUR4WT46DTL2EZMQBCY4SNRF622DN2VODMOYGMSFHMDPP6NW) |
| Anfitrión | `GAAAGOVI3UD4E3BF4YG5EKEP7B36UG26YN6M2FOSC3LM5W37QFNN6SKK` |
| Activo | XLM nativo (SAC `CDLZFC3SYJYDZT7K67VZ75HPJVIEUVNIXF47ZG2FB2RMQQVU2HHGCYSC`) |
| Precio | 1 XLM (`10000000` stroops) |
| Deploy | [tx `de2cf14f…`](https://stellar.expert/explorer/testnet/tx/de2cf14fa6a1548b1e4640f79287a6dffc919a346cd28f909ff15bbb4cc9ca56) |

## Desarrollo

Requiere Rust con el target `wasm32v1-none` y el [Stellar CLI](https://developers.stellar.org/docs/tools/cli/stellar-cli). Desde la raíz del repo:

```bash
cargo test
stellar contract build
```

Los 14 tests cubren la compra (árbol de firmas exacto, evento `bought`, TTL, doble compra, compra a nombre de otro y pago fallido), el check-in (uso único, evento `checked_in`, sin pase, sin firma y firmado por el comprador) y los precios `0` y negativos.

> La fuente principal de este contrato es [latmontecinos-sketch/aex-pass](https://github.com/latmontecinos-sketch/aex-pass): este directorio es una copia para el workspace del programa y tiene que mantenerse igual.

El paso a paso para grabar la demo está en [DEMO.md](DEMO.md).
