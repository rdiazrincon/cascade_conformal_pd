# cascade_conformal_pd
Code for Diaz-Rincon et al 2026 Nat. Mach. Intell. "Improved Prediction of Parkinson’s Disease Medication Needs Through Nested Conformal Prediction"

This notebook implements three strategies for integrating Venn-Abers calibration (Stage 1) with Conformal Prediction (Stage 2):

1. **Baseline**: Standard conformal prediction without using VA information
2. **VA-Stratified**: Separate conformal predictors for each uncertainty category
3. **VA-Augmented**: Include VA probabilities as additional features

### Expected Benefits
- **Better filtering**: Only patients with confident Stage 1 predictions proceed to Stage 2
- **Adaptive intervals**: Stage 2 intervals can adapt based on Stage 1 confidence
- **Clinical interpretability**: Clinicians see both classification confidence and dose prediction uncertainty
- **Efficiency**: Reduced computation and more focused predictions

### Next Steps
1. Compare which integration strategy gives best coverage/efficiency trade-off
2. Analyze subgroup performance (age, disease stage, etc.)
3. Validate on external cohort
4. Consider adaptive alpha based on VA uncertainty