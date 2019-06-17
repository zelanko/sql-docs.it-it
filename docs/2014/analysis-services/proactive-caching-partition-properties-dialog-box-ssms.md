---
title: Attiva la memorizzazione nella cache (finestra di dialogo Proprietà partizione) (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.partitionproperties.proactivecaching.f1
ms.assetid: ecba72a3-703f-4ede-9d85-9a3318a749e5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cb486ec383ab6fa1684bd9d0e9b8f6bc67631eee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070708"
---
# <a name="proactive-caching-partition-properties-dialog-box-ssms"></a>Memorizzazione nella cache attiva (finestra di dialogo Proprietà partizione) (SSMS)
  La pagina **Memorizzazione attiva nella cache** della finestra di dialogo **Proprietà partizione** in SQL Server Management Studio consente di impostare le proprietà di archiviazione e memorizzazione attiva nella cache di una partizione in un gruppo di misure per un cubo in un database di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="options"></a>Opzioni  
 **Impostazione standard**  
 Selezionare questa opzione per attivare il dispositivo di scorrimento per **Impostazione standard** e usare le impostazioni predefinite per le funzionalità relative alla modalità di archiviazione e alla memorizzazione nella cache attiva.  
  
 **Impostazione standard**  
 Consente di specificare una delle impostazioni predefinite elencate nella tabella seguente.  
  
|Impostazione|Descrizione|  
|-------------|-----------------|  
|**ROLAP in tempo reale**|Selezionare questa opzione per utilizzare le impostazioni seguenti per l'archiviazione e la memorizzazione nella cache attiva:<br /><br /> Modalità di archiviazione ROLAP.<br /><br /> Attiva la memorizzazione nella cache attiva.<br /><br /> Elimina la cache obsoleta, con un periodo di latenza di 0 secondi.<br /><br /> Porta l'oggetto online immediatamente.|  
|**HOLAP in tempo reale**|Selezionare questa opzione per utilizzare le impostazioni seguenti per l'archiviazione e la memorizzazione nella cache attiva:<br /><br /> Modalità di archiviazione HOLAP.<br /><br /> Attiva la memorizzazione nella cache attiva.<br /><br /> Elimina la cache obsoleta, con un periodo di latenza di 0 secondi.<br /><br /> Aggiorna la cache in presenza di modifiche ai dati, con un intervallo di inattività di 0 secondi e nessun intervallo di inattività sostitutivo.<br /><br /> Porta l'oggetto online immediatamente.|  
|**MOLAP a bassa latenza**|Selezionare questa opzione per utilizzare le impostazioni seguenti per l'archiviazione e la memorizzazione nella cache attiva:<br /><br /> Modalità di archiviazione MOLAP.<br /><br /> Attiva la memorizzazione nella cache attiva.<br /><br /> Elimina la cache obsoleta, con un periodo di latenza di 30 minuti.<br /><br /> Aggiorna la cache in presenza di modifiche ai dati, con un intervallo di inattività di 10 secondi e un intervallo di inattività sostitutivo di 10 minuti.<br /><br /> Aggiorna la cache in presenza di modifiche ai dati, con un intervallo di inattività di 10 secondi e un intervallo di inattività sostitutivo di 10 minuti.<br /><br /> Porta l'oggetto online immediatamente.|  
|**MOLAP a Media latenza**|Selezionare questa opzione per useBrings oggetto online immediatamente.<br /><br /> l'archiviazione seguente e le impostazioni di memorizzazione nella cache attiva:<br /><br /> Modalità di archiviazione MOLAP.<br /><br /> Attiva la memorizzazione nella cache attiva.<br /><br /> Elimina la cache obsoleta, con un periodo di latenza di 4 ore.<br /><br /> Aggiorna la cache in presenza di modifiche ai dati, con un intervallo di inattività di 10 secondi e un intervallo di inattività sostitutivo di 10 minuti.<br /><br /> Porta l'oggetto online immediatamente.|  
|**MOLAP automatico**|Selezionare questa opzione per utilizzare le impostazioni seguenti per l'archiviazione e la memorizzazione nella cache attiva:<br /><br /> Modalità di archiviazione MOLAP.<br /><br /> Attiva la memorizzazione nella cache attiva.<br /><br /> Aggiorna la cache in presenza di modifiche ai dati, con un intervallo di inattività di 0 secondi e nessun intervallo di inattività sostitutivo.|  
|**MOLAP pianificato**|Selezionare questa opzione per utilizzare le impostazioni seguenti per l'archiviazione e la memorizzazione nella cache attiva:<br /><br /> Modalità di archiviazione MOLAP.<br /><br /> Attivazione della memorizzazione nella cache attiva.<br /><br /> Aggiorna periodicamente la cache, con un intervallo di ricompilazione di 1 giorno.|  
|**MOLAP**|Selezionare questa opzione per utilizzare le impostazioni seguenti per l'archiviazione e la memorizzazione nella cache attiva:<br /><br /> Modalità di archiviazione MOLAP.|  
  
 **Impostazione personalizzata**  
 Selezionare questa opzione per impostare in modo esplicito la modalità di archiviazione, la memorizzazione nella cache attiva e le opzioni di notifica.  
  
 **Opzioni**  
 Fare clic su questo pulsante per visualizzare la finestra di dialogo **Opzioni di archiviazione** e impostare in modo esplicito la modalità di archiviazione, la memorizzazione nella cache attiva e le opzioni di notifica. Per altre informazioni sulla finestra di dialogo **Opzioni di archiviazione**, vedere [Finestra di dialogo Opzioni di archiviazione &#40;Analysis Services - Dati multidimensionali&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md).  
  
## <a name="see-also"></a>Vedere anche  
 [La memorizzazione nella cache &#40;partizioni&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)   
 [Finestra di dialogo proprietà di partizione &#40;SQL Server Management Studio&#41;](partition-properties-dialog-box-ssms.md)   
 [Selezione &#40;finestra di dialogo Proprietà partizione&#41; &#40;SQL Server Management Studio&#41;](selection-partition-properties-dialog-box-ssms.md)   
 [Generale &#40;finestra di dialogo Proprietà partizione&#41; &#40;SQL Server Management Studio&#41;](general-partition-properties-dialog-box-ssms.md)   
 [Configurazione errori per cubi, partizioni e l'elaborazione della dimensione &#40;SSAS - multidimensionale&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
  
