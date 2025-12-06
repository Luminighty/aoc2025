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

---

Array initialization could be improved:
```rs
let s: char[32] = "                               ";
```


---


Exhausting all cases will lead to compilation error, since tile might be an int, even though all cases had returned.
Maybe in this case, we should assert on this?
```rs
fn to_char(tile: Tile): char {
	match tile {
		Tile::SPACE => return '.';
		Tile::PAPER => return '@';
	}
}
```

---

Should throw typecheck error instead of unwrap...
```rs
fn range_size(range: *Range): int {

}
```


---

Add support for never (!)
```rs
extern fn exit(code: int): !

fn parse_op(lexer: *lex::Lexer): bool {
	match lex::curr(lexer) {
		'*' => return mod::Op::Mul;
		'+' => return mod::Op::Add
		_ => {
			std::exit(1);
			// currently have to return here
		}
	}
}
```

---

Add real support for varargs
```rs
// This is not possible currently
std::panic("Unknown operand '%c'", op);
```
