<img src="assets/logo.png" width="112" height="112" alt="Blyx penguin exchanging colored slices between two allocation pies.">

# Turnover

Calculate one-way turnover for two fully allocated long-only weight vectors. This Blyx library is part of the financial data analysis collection.

Netting buys against sells can hide turnover in an allocation comparison. Keep gross directional changes and the one-way budget explicit. [Cvxportfolio, turnover constraints](https://www.cvxportfolio.com/en/1.2.0/constraints.html)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-turnover.git
cd blyx-turnover
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-turnover) · [Package page](https://www.blyx-lang.space/packages/turnover) · [Handbook](https://doc.blyx-lang.space/guide/pintail)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-turnover.git vendor/turnover
```

```blyx
use vendor::turnover::turnover;

fn main() {
    let current = [0.75, 0.25];
    let target = [0.5, 0.5];
    let result = turnover_one_way(current, target);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
0.25
0.25
0.25
```

## API

`turnover_one_way(current, target)`

Returns [one-way turnover, total weight increases, total weight decreases]. Each portfolio must sum to one within 1e-9. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| current | Vector of values, each a probability in [0,1] |
| target | Vector of values, each a probability in [0,1] |

## In use

[Pintail](https://github.com/Rahulchaube1/blyx-pintail) uses this module to compare long-only portfolio snapshots under a one-way turnover budget.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-turnover/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). Read the [artwork notice](assets/NOTICE.txt) for credits.

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
