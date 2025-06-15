+++
title = "The Geometry of LLM Logits (an analytical outer bound)"
date  = "2025-05-29"
+++

---

## 1 Preliminaries

| Symbol                                                | Meaning                                                |
| ----------------------------------------------------- | ------------------------------------------------------ |
| $d$                                                   | width of the residual stream |
| $L$                                                   | number of Transformer blocks |
| $V$                                                   | vocabulary size, so logits live in $\mathbb R^{V}$ |
| $h^{(\ell)}$                                          | residual-stream vector *entering* block $\ell$ |
| $r^{(\ell)}$                                          | the **update** written by block $\ell$ |
| $W\_U\\!\\in\\!\\mathbb R^{V\\times d},\\;b\\in\\mathbb R^{V}$ | un-embedding matrix and bias |

**Additive residual stream.**  
With (pre-/peri-norm) residual connections,

$$
h^{(\ell+1)} \\;=\\; h^{(\ell)} + r^{(\ell)},\\qquad \\ell=0,\\dots,L-1.
$$

Hence the final pre-logit state is the sum of $L+1$ contributions (block 0 = token + positional embeddings):

$$
h^{(L)} = \sum_{\ell=0}^{L} r^{(\ell)}.
$$

---

## 2 Each update is *contained* in an ellipsoid

*Why a bound exists.*  
Every sub-module (attention head or MLP)

1. **reads** a LayerNormed copy of its input, so  
   $\|u\|_2 \le \\rho\_\\ell$ where $\\rho\_\\ell := \\gamma\_\\ell\\sqrt d$ and $\\gamma\_\\ell$ is that block’s learned scale;
2. applies **linear** maps, a **Lipschitz** point-wise non-linearity (GELU, SiLU, …), and another linear map back to $\mathbb R^{d}$.

Because the composition of linear maps and Lipschitz functions is itself Lipschitz, there exists a constant $\\kappa\_\\ell$ such that

$$
\|r^{(\ell)}\|_2 \\;\\le\\; \\kappa\_\\ell
\\qquad\\text{whenever}\\qquad \|u\|_2\\le\\rho\_\\ell.
$$

Define the centred ellipsoid

$$
\\mathcal E^{(\ell)}
\\;:=\\;
\\bigl\\{\,x\\in\\mathbb R^{d}\\;:\\;\\|x\\|_2\\le\\kappa\_\\ell\\bigr\\}.
$$

Then **every realisable update lies inside that ellipsoid**:

$$
r^{(\ell)}\\;\\in\\;\\mathcal E^{(\ell)}.
$$

---

## 3 Residual stream ⊆ Minkowski sum of ellipsoids

Using additivity and Step 2,

$$
h^{(L)}
\\;=\\;\\sum_{\ell=0}^{L} r^{(\ell)}
\\;\\in\\;\\sum_{\ell=0}^{L} \\mathcal E^{(\ell)}
\\;=:\\;\\mathcal E\_{\\text{tot}},
$$

where  
$\\displaystyle
\\sum_{\ell} \\mathcal E^{(\ell)}=
\\mathcal E^{(0)} \\oplus \\dots \\oplus \\mathcal E^{(L)}$
is the **Minkowski sum** of the individual ellipsoids.

---

## 4 Logit space is an affine image of that sum

Logits are produced by the affine map $x\\mapsto W\_U x+b$.  
For any sets $S\_1,\\dots,S\_m$,

$$
W\_U \\Bigl(\\bigoplus\_{i} S\_i\\Bigr)
= \\bigoplus\_{i} W\_U S\_i.
$$

Hence

$$
\\text{logits}
\\;=\\; W\_U h^{(L)} + b
\\;\\in\\; b \\;+\\; \\bigoplus_{\ell=0}^{L} W\_U\\mathcal E^{(\ell)}.
$$

Because linear images of ellipsoids are ellipsoids, each $W\_U\\mathcal E^{(\ell)}$ is still an ellipsoid.

---

## 5 Ellipsotopes

An **ellipsotope** is an affine shift of a finite Minkowski sum of ellipsoids.  
The set

$$
\\boxed{\\;
\\mathcal L\_{\\text{outer}}
\\;:=\\;
b
\\;+\\;
\\bigoplus_{\ell=0}^{L} W\_U\\mathcal E^{(\ell)}
\\;}
$$

therefore *is* an ellipsotope.

---

## 6 Main result (outer bound)

> **Theorem.**  
> For any pre-norm or peri-norm Transformer language model whose blocks receive LayerNormed inputs, the set $\\mathcal L$ of all logit vectors **attainable over every prompt and position** satisfies  
> $$
> \\mathcal L \\;\\subseteq\\; \\mathcal L\_{\\mathrm{outer}},
> $$
> where $\\mathcal L\_{\\mathrm{outer}}$ is the ellipsotope defined above.

*Proof.*  
Containments in Steps 2–4 compose to give the stated inclusion; Step 5 shows the outer set is an ellipsotope. ∎

---

## 7 Remarks & implications

* **It is an *outer* approximation.**  
  Equality $\\mathcal L = \\mathcal L\_{\\text{outer}}$ would require showing that *every* point of the ellipsotope can actually be realised by some token context, which the argument does not provide.

* **Geometry-aware compression and safety.**  
  Because $\\mathcal L\_{\\text{outer}}$ is convex and centrally symmetric, one can fit a minimum-volume outer ellipsoid to it, yielding tight norm-based regularisers or robustness certificates against weight noise / quantisation.

* **Layer-wise attribution.**  
  The individual sets $W\_U\\mathcal E^{(\ell)}$ bound how much any single layer can move the logits, complementing “logit-lens’’ style analyses.

* **Assumptions.**  
  LayerNorm guarantees $\\|u\\|_2$ is bounded; Lipschitz—but not necessarily bounded—activations (GELU, SiLU) then give finite $\\kappa\_\\ell$. Architectures without such norm control would require separate analysis.

---

