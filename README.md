# Programmable 3-Mode Fock-State Interferometer Simulator

This repository contains a compact Jupyter-based simulator for a programmable
three-mode passive photonic interferometer. The simulator uses selectable
Fock-state inputs, three tunable Mach–Zehnder interferometers (MZIs), and
photon-number-resolved (PNR) output measurement.

The purpose is to provide a transparent public example of how phase-programmed
linear optics reshapes many-photon output probability distributions.

## What the simulator demonstrates

The simulator shows that a passive interferometer conserves total photon number,

```math
n_0' + n_1' + n_2' = n_0 + n_1 + n_2,
```

but the probability distribution over the allowed output patterns depends
strongly on the programmed MZI phases. At special phase settings, output states
that are allowed by photon-number conservation can disappear because their
many-photon amplitudes cancel by destructive interference.

This provides a minimal demonstration of:

- programmable photonic interference,
- photon-number conservation,
- photon-number-resolved output sampling,
- MZI phase control,
- interference-based suppression and enhancement of output patterns.

## Interferometer layout

The simulator uses three optical modes and three MZI layers:

```math
(0,1) \rightarrow (1,2) \rightarrow (0,1).
```

Each MZI has one tunable internal phase. The overall mesh unitary is

```math
U_{\mathrm{mesh}}
=
U_{01}^{(2)}(\phi_{01}^{(2)})
U_{12}^{(1)}(\phi_{12}^{(1)})
U_{01}^{(0)}(\phi_{01}^{(0)}).
```

The MZI convention is based on a balanced beamsplitter, an upper-arm phase, and a
second balanced beamsplitter,

```math
\mathrm{MZI}(\phi)=B P(\phi) B,
```

with

```math
B=\frac{1}{\sqrt{2}}
\begin{pmatrix}
1 & i \\
i & 1
\end{pmatrix},
\qquad
P(\phi)=
\begin{pmatrix}
e^{i\phi} & 0 \\
0 & 1
\end{pmatrix}.
```

Up to a global phase, this gives the effective real MZI block

```math
M(\phi)=
\begin{pmatrix}
\sin(\phi/2) & \cos(\phi/2) \\
\cos(\phi/2) & -\sin(\phi/2)
\end{pmatrix}.
```

## Inputs and outputs

The user selects Fock-state inputs

```math
|n_0,n_1,n_2\rangle,
\qquad n_i \in \{0,1\}.
```

The simulator then displays the full PNR output probability distribution over
all output patterns with the same total photon number.

For example, for input

```math
|1,1,0\rangle,
```

the allowed outputs are

```math
|2,0,0\rangle,\ |1,1,0\rangle,\ |1,0,1\rangle,\ |0,2,0\rangle,\ |0,1,1\rangle,\ |0,0,2\rangle.
```

The histogram updates as the MZI phases are changed.

## Permanent-based Fock sampling

For passive linear optics with Fock-state inputs, output amplitudes are governed
by matrix permanents. For input occupation **n** and output occupation **m**,

```math
A_{\mathbf{m},\mathbf{n}}
=
\frac{\mathrm{perm}(U_{\mathbf{m},\mathbf{n}})}
{\sqrt{\prod_i n_i! \prod_j m_j!}},
```

and

```math
P(\mathbf{m}|\mathbf{n}) = |A_{\mathbf{m},\mathbf{n}}|^2.
```

Here \(U_{\mathbf{m},\mathbf{n}}\) is formed by repeating columns of the
interferometer unitary according to the input occupations and repeating rows
according to the output occupations.

This simulator uses Fock-state inputs only. It is therefore distinct from
Gaussian boson sampling with squeezed inputs, where Hafnian- or
Torontonian-based probability formulas arise.

## Repository contents

Suggested repository structure:

```text
.
├── sim_3mode_interference_Fock.ipynb
├── README.md
├── requirements.txt
├── technical_brief.pdf
```

## Requirements

The simulator uses standard Python scientific tools:

```text
numpy
matplotlib
ipywidgets
jupyter
```

Install with:

```bash
pip install numpy matplotlib ipywidgets jupyter
```

Then start Jupyter:

```bash
jupyter lab
```

or

```bash
jupyter notebook
```

## How to run

Open the notebook and run the cells in order.

The notebook is organized as:

- **Cell 1:** tools and physics functions,
- **Cell 2:** user interface and output histogram.

The interface provides:

- three input occupation selectors,
- three MZI phase sliders,
- a photon-number constraint summary,
- a PNR output probability histogram,
- a compact probability table.

## Interpretation

The key point is that zero-probability outputs are not always forbidden outputs.
Some are allowed by photon-number conservation but vanish because of destructive
interference.

This is the basic programmable-photonics effect demonstrated by the simulator:
phase settings in an interferometric mesh control the many-photon output
distribution.

## Relationship to broader work

This simulator is a component-level public artifact. It demonstrates the
programmable-interferometer layer that underlies broader work on photonic
sampling, unitary decomposition, Gaussian boson sampling, continuous-variable
photonic computing, and photonic integrated circuit design.

It is intentionally generic and does not include application-specific feature
encoding, optical scoring, or proposal-specific workflows.

## Acknowledgment

This material was developed and/or adapted with support from the National
Science Foundation through the QCAP-Pilot and QCAP-Design efforts under NSF
Award Nos. OSI-2410813 and OSI-2531569. Any opinions, findings, conclusions, or
recommendations expressed in this material are those of the author(s) and do not
necessarily reflect the views of the National Science Foundation.

## Author

**Boris Kiefer**  
Department of Physics  
New Mexico State University  
[bkiefer@nmsu.edu](mailto:bkiefer@nmsu.edu)

GitHub: [boriskiefer](https://github.com/boriskiefer)  
LinkedIn: [Boris Kiefer](https://www.linkedin.com/in/boris-kiefer-85089831/)
