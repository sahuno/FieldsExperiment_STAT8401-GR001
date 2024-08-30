#mendalian randomization

#load neccessary libraries
library(TwoSampleMR)

#set this in order to access the repository
options(ieugwasr_api = 'gwas-api.mrcieu.ac.uk/')

################## epigenetic study
outcomeID <- "prot-a-707"
library(MRInstruments)
data(gwas_catalog)

#instrument data 
data(aries_mqtl)
MRInstruments::aries_mqtl

#snps at birth
tet_exp_dat <-
  format_aries_mqtl(subset(aries_mqtl, grepl("TET", gene) &
                             age == "Birth"))

tet_exp_dat <-
  format_aries_mqtl(subset(aries_mqtl, grepl("TET", gene) &
                             age == "Middle age"))

#tet_exp_dat <-
#  format_aries_mqtl(subset(aries_mqtl, grepl("TET", gene)))

#clumpiing is not necessary since data coming ftom MRInstruments are already clumped for LD
#tet_exp_dat_clumped <- clump_data(tet_exp_dat)



#set this in order to access the repository
# List available GWASs
#ao <- available_outcomes()

#investigate if there are testis genes
#Immune_instrument <- subset(ao,
#                            grepl("testis",trait))

outcome_dat <- extract_outcome_data(snps=tet_exp_dat$SNP, outcomes = outcomeID)

dat_exposureOutcome <- harmonise_data(tet_exp_dat, outcome_dat)

# Perform MR
res_mQTL <- mr(dat_exposureOutcome)
mr_heterogeneity(dat_exposureOutcome)
mr_pleiotropy_test(dat_exposureOutcome)

##### Experiment 2 #############
#################
# List available GWASs
ao <- available_outcomes()

#check category of outcomes to select. there's disease, risk factors etc..
table(ao$category, ao$subcategory)
table(ao$category,ao$trait)
table(ao$trait)


###step 1:
# Get instruments
exposure_data <- extract_instruments("ieu-a-2")
#no need for clumping;since data came with package

#Step 2: 
# Get effects of instruments on outcome
outcome_data_test <- subset(ao,
                            id == "ieu-a-7")
View(outcome_data_test)
outcome_data <- extract_outcome_data(snps=exposure_data$SNP, outcomes = "ieu-a-7")

# Harmonise the exposure and outcome data
harmonised_data <- harmonise_data(exposure_data, outcome_data)

# Perform MR
result_bmi_chd <- mr(harmonised_data)

mr_heterogeneity(harmonised_data)
mr_pleiotropy_test(harmonised_data)

p1 <- mr_scatter_plot(result_bmi_chd, harmonised_data)
p1[[1]]

#View(epi_instrument)
#View(head(ao, 100)) 
mr_report(harmonised_data)
library(ggplot2)
#set one
#View(ao) 


