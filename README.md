# effect-snippets

VSCode-format snippet pack for the [Effect](https://effect.website) TypeScript ecosystem — covers `Effect`, `Schema`, `Layer`, `Stream`, `Match`, and friends. Activates in `typescript` and `typescriptreact` files.

98 snippets across 16 categories. Short prefixes designed to not collide with LSP module completions (e.g. `suc` not `Effect.s`).

## Installation

The package follows the [friendly-snippets](https://github.com/rafamadriz/friendly-snippets) layout, so any loader that consumes that format works.

### LuaSnip + lazy.nvim

```lua
{
  "L3MON4D3/LuaSnip",
  dependencies = { "rashedInt32/effect-snippets" },
  config = function()
    require("luasnip.loaders.from_vscode").lazy_load()
  end,
}
```

### blink.cmp

```lua
{
  "saghen/blink.cmp",
  dependencies = { "rashedInt32/effect-snippets" },
  opts = {
    snippets = { preset = "luasnip" }, -- if you use LuaSnip
  },
}
```

### nvim-cmp

Same as the LuaSnip block — `cmp_luasnip` will pick the snippets up automatically.

## Conventions

- Tabstops use `$1`, `$2`, …, with `$0` as the final cursor position.
- A few snippets accept both casings via prefix arrays (`tag`/`Tag`, `err`/`Err`) to preserve existing muscle memory.
- Prefixes avoid module-prefixed forms (no `Option.O`) since the LSP already serves those.

## Snippets

### Effect creation

| Prefix | Expands to |
|---|---|
| `suc` | `Effect.succeed(…)` |
| `fail` | `Effect.fail(…)` |
| `die` | `Effect.die(…)` |
| `sync` | `Effect.sync(() => …)` |
| `try` | `Effect.try({ try, catch })` |
| `tryp` | `Effect.tryPromise({ try, catch })` |
| `prom` | `Effect.promise(() => …)` |
| `async` | `Effect.async<A, E>((resume) => …)` |
| `susp` | `Effect.suspend(() => …)` |
| `evoid` | `Effect.void` |
| `enev` | `Effect.never` |

### Generators / functions

| Prefix | Expands to |
|---|---|
| `gen` | `Effect.gen(...)` piped through `Effect.withSpan` |
| `geno` | `Effect.gen(...)` without span |
| `fn` | `Effect.fn(name)(function*)` |
| `fnu` | `Effect.fnUntraced(function*)` |

### Composition

| Prefix | Expands to |
|---|---|
| `map` | `Effect.map((x) => …)` |
| `flat` | `Effect.flatMap((x) => …)` |
| `tap` | `Effect.tap((x) => …)` |
| `tape` | `Effect.tapError((e) => …)` |
| `andt` | `Effect.andThen(…)` |
| `all` | `Effect.all([…], { concurrency })` |
| `each` | `Effect.forEach(…, fn, { concurrency })` |

### Error handling

| Prefix | Expands to |
|---|---|
| `cat` | `Effect.catchAll((e) => …)` |
| `catt` | `Effect.catchTag("Tag", (e) => …)` |
| `catts` | `Effect.catchTags({ … })` |
| `merr` | `Effect.mapError((e) => …)` |
| `orel` | `Effect.orElse(() => …)` |
| `retry` | `Effect.retry({ schedule, times })` |
| `rep` | `Effect.repeat(…)` |
| `eith` | `Effect.either(…)` |
| `exit` | `Effect.exit(…)` |

### Tagged classes & errors

| Prefix | Expands to |
|---|---|
| `err` / `Err` | `class X extends Schema.TaggedError<X>()(...) {}` |
| `derr` | `class X extends Data.TaggedError("X")<{...}> {}` |
| `tcl` | `class X extends Schema.TaggedClass<X>()(...) {}` |
| `treq` | `class X extends Schema.TaggedRequest<X>()(...) {}` |

### Services & Context

| Prefix | Expands to |
|---|---|
| `tag` / `Tag` | `class X extends Context.Tag("X")<X, T>() {}` |
| `gtag` | `Context.GenericTag<T>("X")` |
| `srv` | `class X extends Effect.Service<X>()("X", { effect, dependencies }) {}` |

### Layer & provide

| Prefix | Expands to |
|---|---|
| `lsuc` | `Layer.succeed(Tag, impl)` |
| `leff` | `Layer.effect(Tag, Effect.gen(...))` |
| `lscp` | `Layer.scoped(Tag, Effect.gen(...))` |
| `lmrg` | `Layer.mergeAll(…)` |
| `prov` | `Effect.provide(…)` |

### Schema

| Prefix | Expands to |
|---|---|
| `sst` | `Schema.Struct({ … })` |
| `scl` | `class X extends Schema.Class<X>("X")({ … }) {}` |
| `sarr` | `Schema.Array(…)` |
| `srec` | `Schema.Record({ key, value })` |
| `sopt` | `Schema.optional(…)` |
| `sbr` | `Schema.String.pipe(Schema.brand("X"))` |
| `strn` | `Schema.transform(from, to, { decode, encode })` |
| `sdec` | `Schema.decodeUnknown(…)` |
| `senc` | `Schema.encode(…)` |

### Resource & Scope

| Prefix | Expands to |
|---|---|
| `acq` | `Effect.acquireRelease(acquire, release)` |
| `acqu` | `Effect.acquireUseRelease(acquire, use, release)` |
| `scop` | `Effect.scoped(…)` |
| `fin` | `Effect.addFinalizer((exit) => …)` |

### Concurrency

| Prefix | Expands to |
|---|---|
| `fork` | `Effect.fork(…)` |
| `forkd` | `Effect.forkDaemon(…)` |
| `forks` | `Effect.forkScoped(…)` |
| `race` | `Effect.race(a, b)` |
| `racea` | `Effect.raceAll([…])` |
| `qb` | `Queue.bounded<A>(capacity)` |
| `psb` | `PubSub.bounded<A>(capacity)` |
| `def` | `Deferred.make<A, E>()` |
| `ref` | `Ref.make(…)` |

### Stream

| Prefix | Expands to |
|---|---|
| `smk` | `Stream.make(…)` |
| `sfi` | `Stream.fromIterable(…)` |
| `smap` | `Stream.map((x) => …)` |
| `sflt` | `Stream.filter((x) => …)` |
| `srunc` | `Stream.runCollect` |
| `srund` | `Stream.runDrain` |

### Option / Either / Exit / Chunk

| Prefix | Expands to |
|---|---|
| `osom` | `Option.some(…)` |
| `onon` | `Option.none()` |
| `onul` | `Option.fromNullable(…)` |
| `eri` | `Either.right(…)` |
| `ele` | `Either.left(…)` |
| `xmat` | `Exit.match(exit, { onFailure, onSuccess })` |
| `cof` | `Chunk.of(…)` |

### Pattern matching

| Prefix | Expands to |
|---|---|
| `mv` | `Match.value(x).pipe(Match.tag(...), Match.exhaustive)` |
| `mt` | `Match.type<T>().pipe(...)` |

### Runtime

| Prefix | Expands to |
|---|---|
| `run` | `Effect.runSync(…)` |
| `runp` | `Effect.runPromise(…)` |
| `runpx` | `Effect.runPromiseExit(…)` |
| `runf` | `Effect.runFork(…)` |
| `mrt` | `ManagedRuntime.make(…)` |

### Observability

| Prefix | Expands to |
|---|---|
| `log` | `Effect.log(…)` |
| `logi` | `Effect.logInfo(…)` |
| `logw` | `Effect.logWarning(…)` |
| `loge` | `Effect.logError(…)` |
| `span` | `Effect.withSpan("name")` |
| `annl` | `Effect.annotateLogs({ … })` |
| `anns` | `Effect.annotateSpans({ … })` |

### Type literals

| Prefix | Expands to |
|---|---|
| `eff` | `Effect.Effect<A, E, R>` |
| `opt` | `Option.Option<A>` |
| `lay` | `Layer.Layer<RIn, E, ROut>` |
| `stm` | `Stream.Stream<A, E, R>` |
| `sch` | `Schema.Schema<A, I, R>` |
| `<A` | `<A, E, R>(effect: Effect.Effect<A, E, R>) => …` |

## License

MIT
