# Common Lisp Training

Exercises from a functional programming course in Common Lisp: recursion over lists, closures, higher-order functions, macros, CLOS state machines and a small expression parser.

Year: 2020 · Language: Common Lisp (SBCL) · Context: university coursework (KPI)

## What's inside

Folder names are kept exactly as committed (some contain spaces and parentheses, so quote them in a shell).

| Folder | What it does |
|---|---|
| `lecture-1/` | `my-flatten`, `compose` (two implementations) |
| `lecture-6/` | Convert a string to a hash table and back |
| `lecture-9(awhen aif..)/` | Anaphoric macros `awhen`, `aif` and a `cut` macro (partial application with `_` placeholders) |
| `home-task-1/` | List basics: `sum`, `inc-list`, tail-recursive `my-reverse`, `my-delete-repeats` |
| `home-task-2/` | Bubble, selection and insertion sort, imperative and recursive versions |
| `home-task-3/` | Sets as predicate closures: `create-set`, `my-union`, `my-intersect`, `my-difference` |
| `home-task-4/` | `merge-strings` (interleave), `archieve-string` (run-length encoding, `aaaab` -> `a4b`) |
| `home-task-5/` | Mini SQL-like select over three text tables (`table1-3.txt`: people, buses, links) with `make-select`, in list and hash-table versions; results in `res1-3.txt` |
| `home-task-6/` | Lexer + recursive parser + printer for arithmetic expressions |
| `practice-1/` | `my-remove`, `find-best-element`, `make-mapcar-if`, `assoc-member`, `my-reduce` with `:key`, `:test`, `:from-end`, `:initial-value` |
| `practice-2/` | n-way `merge-strings`, greatest common substring, shortest path down a number triangle (`res.txt` is a generated triangle), greatest palindrome |
| `practice-4(CLOS)/` | State-machine framework in CLOS; instances: conditioner, hair drier, coffee machine |
| `practice-5 (our-let my-or...)/` | Macros `our-let`, `our-let*`, `my-or`, `alambda` |
| `practice-6(with-gensyms, aand...)/` | Macros `with-gensyms`, `aand`, `acond`, `mv-let*` |
| `control-task/` | Control work: n-ary tree (`defstruct node`), traversals, `map-tree`, expression evaluation |

## Interesting bits

- `home-task-6/task6.lisp` parses arithmetic with nested helper functions inside `labels`; tests show it drops redundant parentheses (`"((3 - 2)) - 1"` prints as `"3 - 2 - 1"`).
- `control-task/control-task-ivanenko.lisp` builds a tree from a Lisp form (`(+ 1 2 (* 3 4 5))`), offers pre-order, post-order and breadth-first walks with `:key` and `:mod` callbacks, and evaluates the tree by `apply`-ing the node symbol to its evaluated children.
- `practice-4(CLOS)/task.lisp` (about 640 lines) uses `:before` / `:after` methods on `nextstate` and `send`, and generic `handle-signal` dispatch on state and signal classes; its default method reports unsupported signals.
- `lecture-9(awhen aif..)/task.lisp` `cut` expands `(cut lst a (_ (_)) d _)` into a lambda with one gensym per `_`.

## Run

Verified with SBCL 2.2.9: each file loads cleanly. The test functions print only on failure; with them all were silent (no mismatch):

```
sbcl --noinform --non-interactive --load control-task/control-task-ivanenko.lisp --eval "(tests)"
cd home-task-1 && sbcl --noinform --non-interactive --load work.lisp --eval "(test-all)"
```

Test entry points differ by file (`tests`, `test-all`, `all-tests`); check the end of each file. `home-task-5` reads and writes its `.txt` files in the current directory, so run it from inside that folder.

## Note

Written in 2020, before AI coding assistants. Kept as-is for history.
