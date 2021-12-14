# PNADc
PNADc IBGE


install.packages("PNADcIBGE")

library(PNADcIBGE)

install.packages("survey")

library(survey)

dadosPNADc_brutos = get_pnadc(year = 2020, quarter = 3, vars = c("VD4001", "VD4002"), design = FALSE)

dadosPNADc_brutos

variaveis_selecionadas <- c("UF", "V2007", "V2009", "V2010", "V3007", "VD4001", "VD4002", "VD4020", "VD4035")

dadosPNADc = get_pnadc(year = 2021, quarter = 2, vars = variaveis_selecionadas)

summary(dadosPNADc)

totalrenda <- svytotal(x=~VD4020, design=dadosPNADc, na.rm=TRUE)

totalrenda

cv(object=totalrenda)

totalpopulacional <- svytotal(x=~UF, design=dadosPNADc, na.rm=TRUE)

totalpopulacional

totalsexo <- svytotal(x=~V2007, design=dadosPNADc, na.rm=TRUE)

totalsexo

totalsexoeUF <- svytotal(x=~interaction(V2007,UF), design=dadosPNADc, na.rm=TRUE)

ftable(x=totalsexoeUF)

mediaRendaUF <- svyby(formula=~VD4020, by=~UF, design=dadosPNADc, FUN=svymean, na.rm=TRUE)

mediaRendaUF

svyhist(formula=~as.numeric(VD4020), design=dadosPNADc, main="PNADc", col = "purple", xlab="Média Renda")


