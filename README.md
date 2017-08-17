# regresion17
#variable categorica
#variable factor: contiene variables categoricas, tiene más variables 
#que una varibale categorica

#serobles99

########bajar base de dtos con la misma lógica de la cancion (forma rápida)
temporal<- tempfile()   # meter en un archivo temporal un archivo
download.file("http://www.beta.inegi.org.mx/contenidos/proyectos/enchogares/modulos/mti/2015/microdatos/mti2015_bases_conapo_dbf.zip",temporal)

#fuimos a inegi mti ( trabajo infantil ) clic izquierdo dbf, copiar direccion de enlace
#guarda temporal y como es zip , necesitamos que descomprima

files=unzip(temporal,list=TRUE)$Name
unzip(temporal, files= files[grep("dbf", files)])
library(foreign )
files
mti15<- data.frame(read.dbf("mti2015_05_17_sdem_precodificado.DBF"))
class(mti15$ENT)
mti15$ENT<-as.numeric(mti15$ENT) ### en la base mti a la variable entidad ponla como numerica y vuelve a asignar

class(mti15$ENT)
######como etiquetar una variable poner nombre a diferentes categorias de una variable
##etiquetar

table(mti15$CS_P15)

#en vez de que salga 1 , 2 3 quiero primaria, sec y prepa

mti15$CS_P15<- factor(mti15$CS_P15, levels=c(1,2,3,4),  labels= c("primaria", "secundaria", "preparatoria"," no sabe"))
# etiqueta misma varibale

table(mti15$CS_P15)

##ahora para la variable Rama#####
table(mti15$RAMA)

#en vez de que salga 1 , 2 3 quiero primaria, sec y prepa

mti15$RAMA<- factor(mti15$RAMA, levels=c(1,2,3,4,5,6,7),  labels= c("Agropecuario", "contruccion", "manufacturA"," COMERCIO","SERVICIO", "OTROS","NE"))
# etiqueta misma varibale

table(mti15$RAMA)

###SOLO PARA TRES SECTORES ECONOMICOS PRIMARIO=AGRICULTURA, #SECUNDARIO=MANUFACTURA Y TERCIARIO=COMERCIO

#VAMOS A RECODIFICAR LA VARIABLE RAMA

mti15$RAMA<- as.numeric (mti15$RAMA)
class(mti15$RAMA)
table(mti15$RAMA)

mti15$RAMA[mti15$RAMA==1]<-1
mti15$RAMA[mti15$RAMA==2]<-2
mti15$RAMA[mti15$RAMA==3]<-2
mti15$RAMA[mti15$RAMA==4]<-3
mti15$RAMA[mti15$RAMA==5]<-3
mti15$RAMA[mti15$RAMA==6]<-4
mti15$RAMA[mti15$RAMA==7]<-4
table(mti15$RAMA3)
#DE MI VARIABLE RAMA A MI CATEGORIA 1 LA VUELVO A PONER EN LA 1

mti15$RAMA2<- factor(mti15$RAMA2, levels= c(1,2,3,4), labels=c("primario","secundario","terciario","NE")

