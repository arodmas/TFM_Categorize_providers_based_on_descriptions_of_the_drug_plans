# TFM Categorize providers based on descriptions of the drug_plans
From The National Bureau of economic research data by KSCHOOL – Ángel Rodríguez Masa

 De la página web de la Oficina Nacional de Investigación Económica (The National Bureau of economic research) https://data.nber.org/data/cms-landscape-files-data.html descargo varios ficheros públicos anuales (del 2012 al 2019 incluidos) relacionados con descripciones de los planes de medicamentos de la empresa Medicare en cuanto a ventajas y planes de costos para poder tener una primera estimación de cómo puede calificarse/clasificarse un determinado plan de medicamentos de un proveedor antes de poder llegar a incorporarse en el sistema sanitario de Medicare.
 
Este dataset original se compone de las siguientes variables:

01. state           				      Estado
02. county          				      Condado
03. organizationname 				      Nombre de la organización
04. planname        				      Nombre del plan 
05. typeofmedicarehealthplan		  Tipo de plan para Medicare
06. monthlyconsolidatedpremiumi		Prima mensual consolidada 
07. annualdrugdeductible			    Medicamentos anuales deducicles
08. drugbenefittype 		    	    Tipo de beneficio del medicamento
09. additionalcoverageofferedin		Cobertura adicional ofrecida
10. drugbenefittypedetail			    Detalle del tipo de beneficio
11. contractid      				      ID del contrato
12. planid          				      ID del plan
13. segmentid       				      ID del segmento
14. innetworkmoopamount				    Desembolso máximo
15. overallstarrating				      Calificación general en el sistema sanitario
16. overallstarratingstr 			    Calificación general en el sistema sanitario

Lo que pretendo es predecir la calificación/clasificación de clases, mediante un modelo supervisado de clasificación en Machine Learning a través de la probabilidad más alta de estas clases, referenciadas en la feature origen "overallstarrating" tomando como variables de entrada traducidas:

  names=['ESTADO', 'CONDADO', 'ORGANIZACION', 'TIPO_PLAN_GENERICO_MEDICARE', 'PRIMA_MENSUAL_CONSOLIDADA', 'MEDICAMS_ANUALES_DEDUCIBLES'
         , 'TIPO_BENEFICIO', 'COBERTURA_ADICIONAL_OFRECIDA', 'DETALLE_BENEFICIO', 'DESEMBOLSO_MAXIMO']

y de salida:

  names=['CLASIFICACION'])

por lo que no utilizo (desecho):

  names=['PLAN', 'CONTRAC_ID', 'PLAN_ID', 'SEGMENT_ID', 'CLASIFICACION_STR'])

Para este fin, preparo varios scripts que puedan utilizarse independientemente de la fase en la que nos encontremos e incluso por otras personas que necesiten realizar acciones similares a las descritas.

Se presentan en la ruta relativa '../Repos/TFM_Categorize_providers_based_on_descriptions_of_the_drug_plans/03_Presentation' y son:

También se indica el tiempo de ejecución empleado por cada script
   
01_Loading_and_preprocessing_original_data.ipynb; (84 segs)              
- Cargar y preprocesar los ficheros de datos originales, preparados como ".xlsx" e incluidos en este Repo sobre la estructura de ficheros '../01_Original_data'. Consta de 306183 observaciones.

01_OUT_csv_original_data_transformed.csv; (n/a, se incluye en su proceso padre/origen)                      
- Fichero de salida ".csv" originado al ejecutar el proceso de carga y preprocesado de los ficheros de datos originales que será utilizado por el resto de scripts posteriores.

02_Sample_draw_transformed_data.ipynb; (125 segs)                         
- Dibujar como primera visualización, varias gráficas sobre una muestra de los datos transformados.  

03_Sample_data_preparation_and_pipelines_of_naive_models.ipynb; (36 segs)
- Constructor de varios "pipelines" de cuatro procesos de modelos "naive" sobre una muestra significativa de los datos.

04_Sample_automatic_hyperparameter_search.ipynb; (1 seg)
- Descripción de búsquedas de hyperparámetros sobre muestras de datos mediante Grid Search, que por problemas de recursos, los resultados no se adjuntan en este proyecto.

04a_Sample_ROC_auc_SVC_svm_hyperparameters.ipynb; (26 segs)
- Implementar hyperparámetros manuales sobre muestras de datos para un modelo SVM (Support Vector Machine) con el clasificador Linear SVC (Support Vector Classifier), mostrando gráficas ROC mediante AUC de clases.

04b_Sample_ROC_auc_LOGREG_SAG_hyperparameters.ipynb; (93 segs)
- Implementar hyperparámetros manuales sobre muestras de datos para un modelo de regresión logística con el solver "SAG", mostrando gráficas ROC mediante AUC de clases.

04c_Sample_ROC_auc_LOGREG_NEWTONcg_hyperparameters.ipynb; (11 segs)
- Implementar hyperparámetros manuales sobre muestras de datos para un modelo de regresión logística con el solver "NEWTON_CG", mostrando gráficas ROC mediante AUC de clases.

05_Apply_final_LOGREG_NEWTONcg_model.ipynb; (1814 segs)
- Aplicar el mejor modelo resultante después del tunning de hiperparámetros al conjunto de los datos completos. En este caso, seguimos con un modelo de regresión logística con el solventador "NEWTON_CG", mostrando algunas gráficas que muestran algunas distribuciones y comportamientos de una muestra de los datos.

06_Apply_final_ROC_auc_LOGREG_NEWTONcg_complete.ipynb; (355 segs)
- Implementar el modelo final sobre el conjunto de datos completo para un modelo de regresión logística con el solver "NEWTON_CG", mostrando gráficas ROC mediante AUC de clases.

   
