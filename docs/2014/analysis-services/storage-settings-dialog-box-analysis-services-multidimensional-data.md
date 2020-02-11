---
title: Finestra di dialogo Impostazioni di archiviazione (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.f1
- sql12.asvs.cubeeditor.cubebuilder.measuregroupstoragesettings.f1
ms.assetid: 80c41c71-226c-45fe-b9cf-af824b592fe1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ecd796d2fb2bc37c4c2ad6d9fac00ef4258ec038
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66068033"
---
# <a name="storage-settings-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Impostazioni di archiviazione (Analysis Services - Dati multidimensionali)
  Usare la finestra di dialogo **Impostazioni di archiviazione** di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per impostare la memorizzazione nella cache attiva, la modalità di archiviazione e le impostazioni di notifica per una dimensione, un cubo, un gruppo di misure o una partizione. Per visualizzare la finestra di dialogo **Impostazioni di archiviazione** di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] è possibile:  
  
-   Fare clic sul pulsante con i puntini di sospensione ( `ProactiveCaching` **...**) per il valore della proprietà di una dimensione, un cubo, un gruppo [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]di misure o una partizione nella finestra **proprietà** di.  
  
-   Espandere un gruppo di misure nella scheda **Partizioni** di **Progettazione cubi** e fare clic su **Impostazioni di archiviazione**.  
  
-   Espandere un gruppo di misure e selezionare una partizione nella griglia per tale gruppo di misure nella scheda **Partizioni** di **Progettazione cubi** e fare clic su **Impostazioni di archiviazione**.  
  
-   Espandere un gruppo di misure e selezionare una partizione nella griglia per tale gruppo di misure nella scheda **Partizioni** di **Progettazione cubi** e fare clic su **Impostazioni di archiviazione** nel riquadro **Barra degli strumenti** della scheda **Partizioni** di **Progettazione cubi**.  
  
## <a name="options"></a>Opzioni  
  
|Termine|Definizione|Valori|  
|----------|----------------|------------|  
|**Impostazione standard**|Selezionare questa opzione per attivare il dispositivo di scorrimento per **Impostazione standard** e usare le impostazioni predefinite per le funzionalità relative alla modalità di archiviazione e alla memorizzazione nella cache attiva.||  
|**Impostazione standard**|Consente di impostare una delle impostazioni predefinite seguenti:<br /><br /> **ROLAP in tempo reale**<br /><br /> Selezionare questa opzione per utilizzare le impostazioni seguenti per l'archiviazione e la memorizzazione nella cache attiva:|Modalità di archiviazione ROLAP.<br /><br /> Attivazione della memorizzazione nella cache attiva.<br /><br /> Eliminazione della cache obsoleta, con un periodo di latenza di 0 secondi.<br /><br /> Oggetto online immediatamente.|  
||**HOLAP in tempo reale**<br /><br /> Selezionare questa opzione per utilizzare le impostazioni seguenti per l'archiviazione e la memorizzazione nella cache attiva:|Modalità di archiviazione HOLAP.<br /><br /> Attivazione della memorizzazione nella cache attiva.<br /><br /> Eliminazione della cache obsoleta, con un periodo di latenza di 0 secondi.<br /><br /> Aggiornamento della cache in presenza di modifiche ai dati, con un intervallo di inattività di 0 secondi e nessun intervallo di inattività sostitutivo.<br /><br /> Oggetto online immediatamente.|  
||**MOLAP a bassa latenza**<br /><br /> Selezionare questa opzione per utilizzare le impostazioni seguenti per l'archiviazione e la memorizzazione nella cache attiva:|Modalità di archiviazione MOLAP.<br /><br /> Attivazione della memorizzazione nella cache attiva.<br /><br /> Eliminazione della cache obsoleta, con un periodo di latenza di 30 minuti.<br /><br /> Aggiornamento della cache in presenza di modifiche ai dati, con un intervallo di inattività di 10 secondi e un intervallo di inattività sostitutivo di 10 minuti.<br /><br /> Oggetto online immediatamente.|  
||**MOLAP a media latenza**<br /><br /> Selezionare questa opzione per utilizzare le impostazioni seguenti per l'archiviazione e la memorizzazione nella cache attiva:|Modalità di archiviazione MOLAP.<br /><br /> Attivazione della memorizzazione nella cache attiva.<br /><br /> Eliminazione della cache obsoleta, con un periodo di latenza di 4 ore.<br /><br /> Aggiornamento della cache in presenza di modifiche ai dati, con un intervallo di inattività di 10 secondi e un intervallo di inattività sostitutivo di 10 minuti.<br /><br /> Oggetto online immediatamente.|  
||**MOLAP automatico**<br /><br /> Selezionare questa opzione per utilizzare le impostazioni seguenti per l'archiviazione e la memorizzazione nella cache attiva:|Modalità di archiviazione MOLAP.<br /><br /> Attivazione della memorizzazione nella cache attiva.<br /><br /> Aggiornamento della cache in presenza di modifiche ai dati, con un intervallo di inattività di 0 secondi e nessun intervallo di inattività sostitutivo.|  
||**MOLAP pianificato**<br /><br /> Selezionare questa opzione per utilizzare le impostazioni seguenti per l'archiviazione e la memorizzazione nella cache attiva:|Modalità di archiviazione MOLAP.<br /><br /> Attivazione della memorizzazione nella cache attiva.<br /><br /> Aggiorna periodicamente la cache, con un intervallo di ricompilazione di 1 giorno.|  
||**MOLAP**<br /><br /> Selezionare questa opzione per utilizzare le impostazioni seguenti per l'archiviazione e la memorizzazione nella cache attiva:|Modalità di archiviazione MOLAP.|  
|**Impostazione personalizzata**|Selezionare questa opzione per impostare in modo esplicito la modalità di archiviazione, la memorizzazione nella cache attiva e le opzioni di notifica.||  
|**Opzioni**|Fare clic su questo pulsante per visualizzare la finestra di dialogo **Opzioni di archiviazione** e impostare in modo esplicito la modalità di archiviazione, la memorizzazione nella cache attiva e le opzioni di notifica. Per altre informazioni sulla finestra di dialogo **Opzioni di archiviazione**, vedere [Finestra di dialogo Opzioni di archiviazione &#40;Analysis Services - Dati multidimensionali&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md).||  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Caching attivo &#40;partizioni&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)   
 [Archiviazione di cubi &#40;Analysis Services-Dati multidimensionali&#41;](multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)  
  
  
