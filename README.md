# Evaluating the Transport Impact of Large Post-Quantum DNSSEC Signatures

Group project for the course **Network and Information Systems Security** at
ISCTE – Instituto Universitário de Lisboa.

Post-quantum signature schemes such as ML-DSA-44 (FIPS 204) produce signatures
and public keys that are one to two orders of magnitude larger than the ECDSA
signatures used in DNSSEC today. Signed DNS responses therefore exceed the
1,232-byte EDNS(0) UDP payload recommendation and the typical Internet MTU,
and have to rely on IP fragmentation, truncation with TCP fallback, or
alternative transports. This project studies how these transports behave for
post-quantum DNSSEC.

## Authors

| Name            | Student no. |
|-----------------|-------------|
| Justin Kasper   | 145971      |
| Mert Duman      | 145872      |
| Efim Shchegolev | 144376      |
| Sezer Tetik     | 145873      |

## Research questions

- **RQ1:** How much do ML-DSA-44 signatures increase DNSSEC response sizes,
  packet sizes, and bandwidth consumption, and how often do they trigger
  truncation and TCP fallback, compared with an ECDSA baseline?
- **RQ2:** How do the end-to-end query latency and resource utilization of
  post-quantum DNSSEC with TCP fallback change as path latency and packet loss
  increase?
- **RQ3:** (Time permitting.) To what extent can ARRF or DNS over QUIC reduce
  the overhead identified in RQ1 and RQ2?

## Repository structure

```
.
├── README.md
└── theoretical-part/                     # Project – Part 1 (report)
    ├── DNSSEC_Theoretical_Part_IEEE.tex  # report source (IEEE conference template)
    ├── DNSSEC_Theoretical_Part_IEEE.pdf  # compiled report
    ├── figures/                          # figures used in the report
    ├── IEEEtran.cls                      # IEEE LaTeX class
    └── IEEEtran_HOWTO.pdf                # IEEE template documentation
```

The practical part (Project – Part 2: testbed, measurements, and results) will
be added in a separate directory.

## Building the report

Requires a TeX distribution (e.g. TeX Live or MacTeX) with `latexmk`:

```sh
cd theoretical-part
latexmk -pdf DNSSEC_Theoretical_Part_IEEE.tex
latexmk -c   # optional: remove auxiliary files
```

## Report contents (Part 1)

1. **Introduction** – motivation, problem statement, research questions.
2. **Theoretical Foundations** – DNS and DNSSEC, classical and post-quantum
   signature algorithms, DNS message-size limits (EDNS(0), IP fragmentation,
   truncation and TCP fallback, response sizes, amplification), and transport
   mechanisms (TCP fallback, ARRF, DNS over QUIC), with a round-trip latency
   model.
3. **State of the Art and Related Work** – related work grouped by algorithm
   suitability, TCP fallback alternatives (TurboDNS, QBF, double signatures),
   application-layer fragmentation security, encrypted transports (DoQ), and
   signature-size reduction (MTL mode, differentiated KSK/ZSK), followed by a
   comparative synthesis and the research gap.
4. **Conclusions and Future Work** – summary of findings and the plan for the
   practical part.
