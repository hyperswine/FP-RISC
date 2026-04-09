# FP-RISC

FPR Programming Language.

FPR: Parse -> ANF -> Codegen.

Everything is just pointers in ANF with Ref Counting.

Everything is unboxed except with manual `Box` or `fix` types where you call f again.
You must use explicit recursion with `fix f`.

Require runtime functions:

- type/1
- function/1
- iso/1

Modules like the file itself actually get compiled into a runtime introspectable record that can be read and added on in REI. But does not exist in FP-RISC.
The runtime module thing is really only used with `use/1` that knows how to deal with the compiled artifacts in ~/.fpr.

Preconditions exist at the type level. No post conditions or invariants. Can express most things with only preconditions like

div : Num -> (res: Num) | res != 0.
becomes

type "div" | res != 0 = Num -> (type "res" = Num).

If this fails to unify or evaluate, then type error.

PE exists only in REI. In FP-RISC everything is unboxed and on the stack and copied. Types are resolved statically because they can. Type signatures are optional and just get unified at compile time with the single pass compilation. Type variables technically do exist but also don't. They just get monomorphized for easy compilation.
Local bindings do not need type signatures. Unused polymorphic functions just don't get instantiated.

In FP-RISC everything is linear. There is no forward references or mutual recursion.
