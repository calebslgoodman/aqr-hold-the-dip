# Pandas Notes

- `.rolling(window).max()` creates a trailing-window peak, useful for computing drawdown from the recent high.
- Pandas operations like `fillna()` and `shift()` usually return a new Series, so I need to assign back with `position = position.fillna(0)`.
- `.shift(1)` prevents lookahead bias by making today's return use yesterday's known position.
- A strategy position can be represented as a 0/1 Series, where 1 means invested and 0 means in cash.