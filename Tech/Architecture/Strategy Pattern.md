---
type: atomic
tags: [coding/architecture, coding/patterns, coding/python]
date: 2026-10-04
---

# Strategy Pattern

## Idea
Put each interchangeable way of doing a task behind the same interface, and choose which one to use at runtime. The calling code doesn't change when you add or swap an approach.

## Definition
The **Strategy** pattern defines a family of algorithms, wraps each one in its own object or function with a common signature, and lets the caller pick one without knowing its internals. The caller holds a reference to "something that can do X" and simply calls it. A text-extraction feature is a good example. It defines an OCR interface with one method, `extract(image) -> str`, and provides two implementations: a free on-device OCR engine as the default, and an LLM vision model enabled by a command-line flag for harder images. The rest of the program never mentions either one by name. The same setup supports **primary with fallback**: try the cheap strategy first, and if its confidence is low or it fails, hand the input to the expensive one. In Python this is idiomatic with a `typing.Protocol`, which gives structural typing: any class with a matching `extract` method qualifies, no inheritance needed. In languages with first-class functions a strategy can simply be a function passed as an argument.

```python
class OcrProvider(Protocol):
    def extract(self, image: bytes) -> str: ...
```

## Source
Catalogued in *Design Patterns: Elements of Reusable Object-Oriented Software* by Gamma, Helm, Johnson and Vlissides (the "Gang of Four"), Addison-Wesley, 1994, where it is also called "Policy".

---

## Compass

**Roots** — *where this comes from*
It is one of the behavioural patterns in [[Design Patterns (Gang of Four)]], and in [[Python]] protocols make it lightweight enough to use without class hierarchies.

**Paths** — *where this leads*
In .NET, a [[Keyed Service (DI)]] lets the container hold several strategies and resolve one by name, and [[Selective LLM Usage]] is the strategy choice of when to pay for a model at all.

**Neighbors** — *what lives nearby*
[[Ports and Adapters]] applies the same plug-in idea at the level of whole external systems, and [[Dependency Injection]] is how the chosen strategy usually reaches the code that uses it.

**Clash** — *what pushes against this*
With only one real implementation, a strategy interface is speculative design; the [[Rule of Three]] says wait. And a fallback chain can hide that the primary path is failing most of the time unless you log which strategy actually ran.
