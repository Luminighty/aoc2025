# Advent of Code 2026

My solutions to Advent of Code 2026 using `iblang` the language I'm developing.

---

## Oddities found:


```rs
// Having to force reference global constant strings when passing to printf
const TITLE = "TEST";
fn main() {
    std::printf("--- %s ---\n", &TITLE);
}
```


---


Autodereffing kinda breaks here, but it's kinda expected?
```rs
fn apply_rotation(state: *int, rotation: *Rotation) {
    //state = state + v;
    *state = *state + v;
}
```

---

char -> int conversion may have unexpected behaviour due to unsigned -> signed
```rs
let v = 0;
let d: int = curr(lexer) - '0';
v = (v * 10) + d;
```
