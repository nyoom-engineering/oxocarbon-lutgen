# Oxocarbon Image Batch Processor

> Ultra-fast, palette-accurate colour-grading for images – powered by the **Oxocarbon** palette and written in OCaml/OxCaml.

You should probably use lutgen-rs, the output is the same, but this one is fun

<figure>
  <img alt="ries-t2" width="375" src="./out/ries-t2.png" />
  <figcaption>ries-t2</figcaption>
</figure>

<br>
<br>

<figure>
  <img alt="ries-t" width="375" src="./out/ries-t.png" />
  <figcaption>ries-t</figcaption>
</figure>

<br>
<br>

<figure>
  <img alt="med-gr-l-4" width="375" src="./out/med-gr-l-4.png" />
  <figcaption>med-gr-l-4</figcaption>
</figure>

<br>
<br>

<figure>
  <img alt="lar-gr-l-13" width="375" src="./out/lar-gr-l-13.png" />
  <figcaption>lar-gr-l-13</figcaption>
</figure>

<br>
<br>

<figure>
  <img alt="lar-gr-l-7" width="375" src="./out/lar-gr-l-7.png" />
  <figcaption>lar-gr-l-7</figcaption>
</figure>

<br>
<br>

<figure>
  <img alt="lar-gr-l-1" width="375" src="./out/lar-gr-l-1.png" />
  <figcaption>lar-gr-l-1</figcaption>
</figure>

<br>
<br>

<figure>
  <img alt="champ2" width="375" src="./out/champ2.png" />
  <figcaption>champ2</figcaption>
</figure>

<br>
<br>

<figure>
  <img alt="a-root-rtt-05-key" width="375" src="./out/a-root-rtt-05-key.png" />
  <figcaption>a-root-rtt-05-key</figcaption>
</figure>

<br>
<br>

## Features

* One-time LUT build – A dense HALD‐4 lookup-table is generated once using Gaussian-RBF interpolation in Oklab space and cached.
* Blazing-fast processing – Allocation-free, inlined trilinear filtering & parallelism chew through whole folders of PNGs in seconds.
* Optional luminance weighting and preserve

## Installation

### Dependencies

* [OxCaml](https://oxcaml.org/get-oxcaml/)
* [`opam`](https://opam.ocaml.org) with the following libraries:
  * `imagelib` (`imagelib.unix` flavour)
  * `domainslib`

A one-liner to obtain everything on a new switch:

```bash
opam update --all
opam switch create 5.2.0+ox --repos ox=git+https://github.com/oxcaml/opam-repository.git,default
eval $(opam env --switch 5.2.0+ox)
opam install -y ocamlformat merlin ocaml-lsp-server utop parallel core_unix
opam install -y imagelib domainslib
```

### Run

```bash
# inside the caida/ directory
make          # compiles img_oxocarbon, runs on caida-original/ and puts results in out/
make run      # builds (if needed) and colour-grades all PNGs in caida-original/ → out/

# or manually
ocamlfind ocamlopt -O3 -thread -unsafe \
  -package imagelib.unix,domainslib -linkpkg \
  -o img_oxocarbon img_oxocarbon.ml

./img_oxocarbon <input_dir> <output_dir>
```

Optionally use `--invert` to invert the input image, `--preserve` to preserve luminance, and set `OXO_LUM_FACTOR` to adjust luminance

## License

This project is vendored under the MIT liscense

The Oxocarbon palette belongs to its respective authors; used here under the same terms as the original theme.

## Acknowledgements

* [Björn Ottosson](https://bottosson.github.io/) – Author of Oklab perceptual colour space.
* [Ozwaldorf](https://github.com/ozwaldorf/lutgen-rs/tree/main) - Author of lutgen-rs
* [Caida](https://www.caida.org) - Source of sample images