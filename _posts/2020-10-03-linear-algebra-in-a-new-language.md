---
layout: post
title: Linear algebra in a new language
category: devlog
tags:
- algebra
- zig
date: 2020-10-03 17:15 +0200
---
For reasons unknown, I stumbled onto the [Zig] programming language, a new, still in development, low-level systems programming language; like C, but without all the bad things. So I guess quite different from C, but syntax is similarish. It uses LLVM as compiler backend, so it pretty much runs on everything less than 20 years old, and crosscompiles like that's what you always do.

I decided to write a nice generic API for the subset of Linear Algebra that's needed for 3D computer graphics, in case I want to write another raytracer in the near future, and optimize for performance this time.

```zig
test "vector cross product" {
    const x = vector([_]f32{ 1.0, 0.0, 0.0 });
    const y = vector([_]f32{ 0.0, 1.0, 0.0 });
    const z = vector([_]f32{ 0.0, 0.0, 1.0 });

    expectEqual(x, y.cross(z));
    expectEqual(y, z.cross(x));
    expectEqual(z, x.cross(y));
}
```

One very cool feature that makes this possible in a statically typed, [AOT] compiled language is that the compiler actually interprets as much of the code it can at compile time, making the language meta-programmable in itself.

```zig
// return anytype inference is currently a TODO compiler error so
// the switch on type must be duplicated instead
pub fn vector(arg: anytype) anytype {
    return (switch (@typeInfo(@TypeOf(arg))) {
        .Array => |t| VecT([t.len]t.child),
        .Vector => |t| VecT([t.len]t.child),
        else => @compileError("cannot cast from " ++ @typeName(@TypeOf(arg))),
    }).cast(arg);
}
```

This constructor takes any array slice of a numeric type, or a SIMD vector, and casts into a matching `struct{x:f32, ...}` value, for convenient element access. Because types are first-class values at comptime, this is done at comptime, and reduces to `VecT(...).cast(...)`, and futher on because the actual value of `arg` does not need to be known, only its type, so those functions are also evaluated at comptime, creating the proper type `struct{x:f32, ...}` with specialized versions of all generic functions. Then the specialized `cast()` function, still at comptime, does type coersion and safely reinterprets the value as itself. Any errors found are raised as compile errors, with a proper call trace of how it got there, instead of just the file name and line number.

```zig
const Simd = std.meta.Vector(@This().len, @This().T);

pub fn cross(u: @This(), v: @This()) @This() {
    if (use_simd) {
        const u_yzx: Simd = .{ u.y, u.z, u.x };
        const u_zxy: Simd = .{ u.z, u.x, u.y };
        const v_yzx: Simd = .{ v.y, v.z, v.x };
        const v_zxy: Simd = .{ v.z, v.x, v.y };

        return @This().cast(u_yzx * v_zxy - u_zxy * v_yzx);
    } else {
        return @This(){
            .x = u.y * v.z - u.z * v.y,
            .y = u.z * v.x - u.x * v.z,
            .z = u.x * v.y - u.y * v.x,
        };
    }
}
```

The `cross()` function is comptime specialized for the `@This()` type, and allows conditional compilation of the SIMD or non-SIMD implementation. And again the `Simd` data type is also specialized at comptime with help of the meta programming submodule of the standard library. Due to lazy evaluation at comptime, this only happens if the SIMD version is compiled, with no need for extra guards to avoid dead code.

If we want to run benchmarks to see of the attempted SIMD optimization gave any performance boost, we can simple instanciate all the versions of the vector type and compare.

```zig
Benchmark                          Mean(ns)
-------------------------------------------
cross_cold([3]f16, SIMD)              6.149
cross_cold([3]f32, SIMD)              1.619
cross_cold([3]f64, SIMD)              1.708
cross_cold([3]f16, non-SIMD)          4.245
cross_cold([3]f32, non-SIMD)          1.247
cross_cold([3]f64, non-SIMD)          1.080
cross_hot([3]f16, SIMD)               0.842
cross_hot([3]f32, SIMD)               0.840
cross_hot([3]f64, SIMD)               0.832
cross_hot([3]f16, non-SIMD)           0.847
cross_hot([3]f32, non-SIMD)           0.841
cross_hot([3]f64, non-SIMD)           0.897
```

It seems like that when data is hot in the cache, it doesn't really matter, but cold data has much worse performance for the SIMD implementation, so that SIMD shuffle load code needs some work, and even then this particular operation doesn't gain anything, at least not on this i7 CPU.

Running the same language dynamically interpreted at compile time, as statically at runtime really is the best of both worlds; the blazing runtime speed of a static language, and most of the in-language meta programming capabilities of a dynamic language.

[zig]: https://ziglang.org
[AOT]: https://en.wikipedia.org/wiki/Ahead-of-time_compilation
