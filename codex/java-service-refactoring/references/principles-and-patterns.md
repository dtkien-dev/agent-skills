# Principles and patterns

Use SOLID and named refactorings as diagnostics:

| Signal | Useful question | Do not conclude |
| --- | --- | --- |
| Single responsibility | Do independent reasons to change force unrelated edits in this unit? | Every method needs its own class. |
| Open/closed | Does a repeated conditional have stable variants and a real extension point? | Every `if` needs Strategy. |
| Substitution | Can implementations preserve the caller's expected preconditions, results, and errors? | An interface alone proves substitutability. |
| Interface segregation | Is a consumer forced to depend on unrelated operations? | Splitting every interface improves design. |
| Dependency inversion | Is high-level business policy coupled directly to unstable infrastructure? | Every dependency needs an abstraction. |

Consider Extract Method/Class, Move Method, Replace Conditional with Polymorphism, Introduce Parameter Object, or Replace Magic Number only when it lowers a demonstrated cost and the target architecture has evidence for it. Prefer deletion and direct reuse over adding abstractions. Never use a named pattern to hide a missing business decision or an unclear transaction/authorization boundary.
