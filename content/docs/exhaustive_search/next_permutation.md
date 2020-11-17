---
title: "Test"
date: 2020-11-17T00:33:37+09:00
tags: ["test"]
---

# next_permutation

## 概要

与えられた拝謁の、次の順列を生成します。はじめにソートされている必要があります。

## 使用例

```rs
fn main() {
    let mut x = vec![3.14, -1.25, 4.4];
    x.sort_by(|a, b| a.partial_cmp(b).unwrap());
    
    assert_eq!(x, vec![-1.25, 3.14, 4.4]);

    while {
        println!("{:?}", x);

        next_permutation(&mut x)
    } {}
}

```

```
output:
[-1.25, 3.14, 4.4]
[-1.25, 4.4, 3.14]
[3.14, -1.25, 4.4]
[3.14, 4.4, -1.25]
[4.4, -1.25, 3.14]
[4.4, 3.14, -1.25]
```

## 実装

```rs
fn next_permutation<T: PartialOrd>(v: &mut [T]) -> bool {
    let mut i: i64 = -1;
    let mut j: usize = 0;

    for (idx, e) in v.iter().enumerate() {
        if idx == v.len() - 1 {
            break;
        }
        if *e < v[idx + 1] {
            i = idx as i64;
        }
    }

    if i == -1 {
        return false;
    };

    let i = i as usize;

    for (idx, e) in v.iter().enumerate().rev() {
        if *e > v[i] {
            j = idx;
            break;
        }
    }

    v.swap(i, j);
    v[i + 1..].reverse();

    true
}
```