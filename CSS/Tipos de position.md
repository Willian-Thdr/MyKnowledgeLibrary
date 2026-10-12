| `position` |     Fluxo normal? | Referência principal  | Pode usar `top/left`? |
| ---------- | ----------------: | --------------------- | --------------------: |
| `static`   |               Sim | Layout normal         |                    ❌ |
| `relative` |               Sim | Sua posição original  |                    ✅ |
| `absolute` |               Não | Ancestral posicionado |                    ✅ |
| `fixed`    |               Não | Viewport              |                    ✅ |
| `sticky`   | Sim, inicialmente | Scroll + ancestral    |                    ✅ |
