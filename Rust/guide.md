## Commonly used attribute in Rust

| Attribute                         | Purpose                                                             |
| --------------------------------- | ------------------------------------------------------------------- |
| `#[allow(lint_name)]`             | Suppress a specific warning (e.g., `unreachable_code`, `dead_code`) |
| `#[deny(lint_name)]`              | Turn a lint into a compiler **error**                               |
| `#[warn(lint_name)]`              | Ensure a specific lint shows a warning (even if normally off)       |
| `#[cfg(...)]`                     | Configuration. Conditionally include code based on features, OS, etc.              |
| `#[cfg_attr(...)]`                | Apply an attribute conditionally                                    |
| `#[derive(...)]`                  | Automatically implement traits like `Debug`, `Clone`, etc.          |
| `#[repr(...)]`                    | Control memory layout (e.g., `C`, `packed`, `transparent`)          |
| `#[inline]` / `#[inline(always)]` | Hint to the compiler to inline a function                           |
| `#[test]`                         | Marks a function as a test                                          |
| `#[macro_export]`                 | Expose a macro to other crates                                      |
| `#[no_std]`                       | Compile without the standard library                                |
