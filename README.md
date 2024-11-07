# Kinetik Modelling for Gene Expression System

Repository ini berisi model matematis yang mensimulasikan dinamika sistem ekspresi gen LhGR-Dexamethasone-TMV. Model ini diimplementasikan menggunakan Python dan menggunakan ODE untuk menggambarkan sistem.

## Gambaran Sistem

Model ini menggambarkan interaksi antara
* LhGR (faktor transkripsi)
* pOp6 (promotor)
* Dexamethasone (inducer)
* TMV Replicase (target gen)

Sistem ini mencakup proses transkripsi, translasi, pengikatan, dan degradasi.

## Komponen Model

Model ini menggambarkan lima variabel:
* mRNA_LhGR: konsentrasi mRNA LhGR
* LhGR: Konsentrasi protein LhGR bebas
* Dex: Konsentrasi Dexamethasone bebas
* Dex_LhGR: Konsentrasi kompleks Dexamethasone-LhGR
* TMV: Konsentrasi protein TMV

## Parameter Model

Kinetik model menggunakan parameter berikut:
* k_transcr_LhGR: laju transkripsi
* k_degrad_mRNA: laju degradasi mRNA
* k_transl_LhGR: laju translasi
* k_degrad_LhGR: laju degradasi protein
* k_on: laju pengikatan
* k_off: laju pelepasan
* Kd: konstanta disosiasi
* n: Koefisien Hill
* alpha: laju produksi TMV maksimal
* k_degrad_TMV: laju degradasi TMV

## Persamaan Model

Sistem ini dijelaskan oleh persamaan differensial berikut:
![ODE Kinetik Model][def]

[def]: image.png

dan digambarkan pada bagian code berikut:
```
    dmRNA_LhGR_dt = k_transcr_LhGR * gene_LhGR - k_degrad_mRNA * mRNA_LhGR
    dLhGR_dt = k_transl_LhGR * mRNA_LhGR - k_degrad_LhGR * LhGR - k_on * Dex * LhGR + k_off * Dex_LhGR
    dDex_dt = -k_on * Dex * LhGR + k_off * Dex_LhGR
    dDex_LhGR_dt = k_on * Dex * LhGR - k_off * Dex_LhGR
    dTMV_dt = (alpha * (Dex_LhGR**n)/(Kd + Dex_LhGR**n)) - k_degrad_TMV * TMV
```