# Defining genetic mechanisms of insulin resistance that shape fat partitioning and cardiometabolic disease risk

Repository to showcase the preliminary results for the project proposed for Danish Diabetes and Endocrine Academy (DDEA)'s postdoctoral fellowship of 2026.

## Brief background, hypothesis and aims:

From our previous analyses reported in medRxiv (currently under review in Nature Metabolism) [1], we identified 282 insulin resistance (IR)-associated loci utilizing multi-trait genome-wide association studies (GWAS) approaches that leveraged GWAS from body mass index adjusted fasting insulin levels (FIadjBMI) [2], high density lipoprotein cholesterol (HDL) and triglycerides (TG) [3] (nmax=1.25).Consistent with the adipose tissue expandability hypothesis, IR-increasing alleles across these loci were associated with reduced gluteofemoral subcutaneous adipose tissue (GSAT) and increased fat accumulation in visceral adipose tissue (VAT), liver, and skeletal muscle. These findings support the concept that limited capacity for subcutaneous fat storage promotes lipid spillover into ectopic tissues, contributing to systemic insulin resistance, inflammation, and cardiometabolic disease risk.

*However we also identified heterogeneity across the 282 IR-associated loci*. We identified three distinct groups with different fat distribution profiles: (1) 141 loci associated with decreased GSAT and increased liver fat, (2) 63 loci associated with decreased abdominal and gluteofemoral subcutaneous fat (ASAT and GSAT) together with increased liver and muscle fat, and (3) 78 loci associated with increased fat across all measured depots. Notably, these groups also differed in regulatory enrichment patterns during adipogenesis, with the first subgroup enriched in mature adipocyte regulatory regions (day 14) and the second subgroup enriched in immature adipocyte regulatory regions (day 4). 

From these results **we hypothesize that IR-associated loci can be partitioned into biologically distinct subgroups that differentially influence fat distribution across adipose and ectopic depots.** These fat distribution phenotypes likely arise through diverse molecular mechanisms, including processes acting at different stages of adipogenesis. Consequently, distinct IR mechanisms may confer differential susceptibility to cardiometabolic diseases and represent unique therapeutic targets.

Thus, the main aim of this project is to **identify genetically distinct mechanisms of IR that differentially influence fat distribution across adipose and ectopic depots and determine their clinical consequences and underlying molecular mechanisms.**

With these preliminary results **I aim to highlight to reviewers a novel pipeline that focuses on better identifying subgroup of IR loci with distinct effects of fat distribution, showing that they each contribute to the adipose tissue expandability hypothesis through different mechanisms.** Knowing these mechanisms might help prioritize individuals at different risks of distinct cardiometabolic disease and might help identify more specific and effective drug targets the strengths of our pipeline, providing confidence in the results that we can find and that those can be achieved in the two-year time.**

## Methods:

### Multi-trait IR-fat distribution associations

We used GWAS summary statistics for TG/HDL (n = 402,398) and BMI- and height-adjusted MRI-derived measures of ASAT, GSAT, VAT [4], liver fat, and thigh muscle fat infiltration [5] (nmax = 38,965). We utilized BMI- and height-addjusted GWAS to identify loci influencing body fat distribution independent of overall adiposity. We then applied the PLACO+ a pairwise multi-trait framework [6] to identify loci jointly associated between TG/HDL and each MRI-derived fat volume trait. In PLACO+, the null hypothesis assumes that the variant affects at most one trait, while the alternative hypothesis is that the variant contributes to variation in both traits, providing evidence for a shared genetic mechanism.

To maximize discovery while ensuring robustness, loci were required to meet three criteria: (i) association with TG/HDL at P < 5 × 10⁻⁵, (ii) association with the fat depot trait at P < 0.05, and (iii) genome-wide significant evidence of joint association from PLACO+ (P < 5 × 10⁻⁸). This approach increases power to detect shared genetic determinants while minimizing the inclusion of false-positive signals driven by a single trait.

### LD-based identification of independent loci

To identify independent IR-associated loci, we performed linkage disequilibrium (LD) clumping using the ld_clump_local() function implemented in the ieugwasr package [X]. The function utilizes PLINK v1.9 [X] to identify approximately independent association signals based on pairwise LD. LD was estimated using the European ancestry reference panel from the 1000 Genomes Project Phase 3 release (version 5), consisting of 503 individuals [X]. Clumping analyses were restricted to TG/HDL variants that satisfied the multi-trait association criteria described above. LD clumping was performed using an LD threshold of r² < 0.01 and a clumping window of ±1 Mb (1,000 kb).

### Identifying IR subgroups with distinct effects on fat distirbution

We applied the NavMix hard-clustering algorithm to all independent TG/HDL loci that showed evidence of joint association with at least one fat volume trait (PLACO+ P < 5 × 10⁻⁸). For each locus, effect estimates for ASAT, GSAT, VAT, liver fat, and thigh muscle fat infiltration were aligned to the TG/HDL-increasing allele and converted to z-scores. NavMix utilizes these standardized effect estimates to identify clusters of variants with similar association profiles while accounting for both the magnitude and direction of effects across traits. Loci exhibiting comparable patterns of fat distribution were therefore grouped into the same cluster. To distinguish loci characterized primarily by their fat distribution profile from those whose clustering might be driven by strong TG/HDL associations, we additionally included TG/HDL z-scores in the clustering framework. This approach was intended to mitigate the potential influence of large differences in statistical power between TG/HDL and imaging-derived phenotypes, which can affect the interpretation of multi-trait association results. The number of clusters was determined automatically by NavMix according to its model selection procedure. All remaining clustering parameters were left at their default settings.

### Validation of IR subgroup associations

To validate whether the identified IR subgroups were associated with insulin resistance and distinct fat distribution patterns, we performed polygenic risk score (PRS) analyses using the grs.summary() function from the gtx package (version 0.0.8). This function estimates the aggregate genetic effect of a set of variants on an outcome trait using GWAS summary statistics, providing a summary-statistics-based approximation of a PRS. As the exposure, we used all independent TG/HDL-increasing lead variants within each IR subgroup. As outcomes, we utilized GWAS summary statistics for 4 glycemic traits and 7 anthropometric and fat distribution traits [X, X, X, X]. Associations were aligned to the TG/HDL-increasing allele such that positive effect estimates reflected a higher genetic burden of the corresponding IR subgroup

### Enrichment analyses: 

To investigate the biological mechanisms underlying the identified IR subgroups, we performed functional enrichment analyses following the approach described by Lotta et al. [X]. This method assesses whether a set of loci overlaps a given functional annotation more frequently than expected by chance using a binomial test-based framework. Specifically, the observed overlap between loci of interest and a functional annotation is compared against the overlap observed for matched sets of independent loci with similar genomic characteristics. Matching is performed on locus size, proxy variant density, and distance to the nearest gene transcription start site (TSS), thereby accounting for potential confounding due to genomic architecture. Using this framework, we tested whether each IR subgroup was enriched for active enhancer regions defined by the 15-state chromatin model across 98 ROADMAP Epigenomics tissues and cell types [X]. We additionally evaluated enrichment within differentially accessible chromatin regions derived from adipose tissue and SGBS adipocyte differentiation experiments, including day 0 (preadipocytes), day 4 (immature adipocytes), and day 14 (mature adipocytes), as well as regions exhibiting greater chromatin accessibility in VAT relative to SAT and in SAT relative to VAT [REF]. Statistical significance was assessed using 1 million matched permutations. Enrichment was considered significant when the Benjamini-Hochberg (BH) false discovery rate-corrected P-value was < 0.05.

## Results:

To identify subgroups of IR loci with distinct effects on fat distirbution 

## Discussion:

## References:

1) Garcia-Urena M, Toh PJY, Sanz Martinez R, Kaalia R, Murali M, Dashti H, Jing Y, Cunha C, Romero-Lado MJ, Huang Y, Wabitsch M, Claussnitzer M, Kilpeläinen TO. Genome-Wide Discovery Reveals Adipose-Specific and Systemic Regulators of Insulin Resistance. medRxiv [Preprint]. 2026 Apr 1:2026.03.31.26349822. doi: 10.64898/2026.03.31.26349822. PMID: 41959785; PMCID: PMC13060440.
2) Chen J, Spracklen CN, Marenne G, Varshney A, Corbin LJ, Luan JMeta-Analysis of Glucose and Insulin-related Traits Consortium (MAGIC). The trans-ancestral genomic architecture of glycemic traits. Nat Genet. 2021 Jun;53(6):840-860. doi: 10.1038/s41588-021-00852-9. Epub 2021 May 31. PMID: 34059833; PMCID: PMC7610958.
3) Graham SE, Clarke SL, Wu KH, Kanoni S, Zajac GJM, Ramdas SThe power of genetic diversity in genome-wide association studies of lipids. Nature. 2021 Dec;600(7890):675-679. doi: 10.1038/s41586-021-04064-3. Epub 2021 Dec 9. Erratum in: Nature. 2023 Jun;618(7965):E19-E20. doi: 10.1038/s41586-023-06194-2. PMID: 34887591; PMCID: PMC8730582.
