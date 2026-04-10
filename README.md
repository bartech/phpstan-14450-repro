# PHPStan 2.1.29+ regression: transitive `jetbrains/phpstorm-stubs` overrides internal stubs

Minimal reproduction for [phpstan/phpstan#14450](https://github.com/phpstan/phpstan/issues/14450).

## Setup

- `phpstan/phpstan` — the tool
- `lucasbustamante/stubz` — a dev tool that transitively pulls in `jetbrains/phpstorm-stubs` via `roave/better-reflection`

No direct dependency on `jetbrains/phpstorm-stubs`. No reference to it in `phpstan.neon`.

## Reproduce

```bash
composer install
vendor/bin/phpstan analyse --level=2 -c phpstan.neon
# 2.1.29+: 2 errors
# 2.1.28:  0 errors
```

## Verify fix with 2.1.28

```bash
composer require --dev phpstan/phpstan:2.1.28
vendor/bin/phpstan clear-result-cache -c phpstan.neon
vendor/bin/phpstan analyse --level=2 -c phpstan.neon
# 0 errors
```
