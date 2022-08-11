# zignite
zignite is a lazy stream library for Zig.

## Example Code

* The following code does **not** generate an intermediate collection.
* The following code compiles to a single While statement.
* However, removing the `sum` method only produces the initial state of the iterator, not a While statement.

```README.example.zig
const zignite = @import("src/zignite.zig");
const std = @import("std");

fn even(x: usize) bool {
    return @mod(x, 2) == 0;
}

const RepeatTake = zignite.Repeat(usize).Take();
fn repeat_take(x: usize) RepeatTake {
    return zignite.repeat(usize, x).take(x);
}

test "Example Code" {
    const x = zignite
        .range(usize, 0, 100) //              { 0, 1, ..., 99 }
        .filter(even) //                      { 0, 2, ..., 98 }
        .flatMap(RepeatTake, repeat_take) // { 2, 2, 4, 4, 4, 4, ..., 98 }
        .sum();

    try std.testing.expect(x == 161700);
}
```

## Test code and implementation

* [empty](./src/producer/empty.zig)
* [from_slice](./src/producer/from_slice.zig)
* [once](./src/producer/once.zig)
* [range](./src/producer/range.zig)
* [repeat](./src/producer/repeat.zig)
* [filter](./src/prosumer/filter.zig)
* [flat_map](./src/prosumer/flat_map.zig)
* [take](./src/prosumer/take.zig)
* [fold](./src/consumer/fold.zig)
* [is_empty](./src/consumer/is_empty.zig)
* [sum](./src/consumer/sum.zig)
* [to_slice](./src/consumer/to_slice.zig)
