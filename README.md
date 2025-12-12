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



---

Weird pass struct by value error

```rs
pub struct Vec3 {x: int, y: int, z: int}
let box_c = 100;
let boxes = std::malloc(sizeof(Vec3) * box_c);

for let i = 0; i < box_count; i+=1 {
for let j = i + 1; j < box_count; j+=1 {
	// Before calling this, it segfaults
	let d = distance(boxes[i], boxes[j]);
}}

fn distance(left: Vec3, right: Vec3): int {
	let dx = left.x - right.x;
	let dy = left.y - right.y;
	let dz = left.z - right.z;
	return (dx * dx) + (dy * dy) + (dz * dz);
}
```

---


Have to prealloc the stack at the start of funcs

```rs
// This would slowly fill the stack with copies of "Hello World\n" instead of reusing the same space. :(
for let i = 0; i < 1000; i+=1 {
for let j = 0; j < 1000; j+=1 {
for let k = 0; k < 1000; k+=1 {
	let v = "Hello World\n";
	std::printf("Hello World\n");
}}}
```


---

handle for duplicate names:

```rs
const filename = "./inputs/day11.txt";
const filename = "./inputs/day11_ex.txt";

cc error: ./build/src_day11_input.ib.s: Assembler messages:
./build/src_day11_input.ib.s:27: Error: symbol `s234_filename' is already defined
```

---

I think this is invalid:

```rs
let tile = [
	false,false,false,
	false,false,false,
	false,false,false
];
return mod::Shape { tile, count };
```
