---
title: Finestra di dialogo Proprietà (SSAS - multidimensionale) del database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.databaseproperties.f1
ms.assetid: 70f000b7-917f-4699-b142-7a0d13ff767c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a18669d646dcf6e46f609faeb0861e5fa9732850
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62732570"
---
# <a name="database-properties-dialog-box-ssas---multidimensional"></a>Finestra di dialogo Proprietà database (SSAS - Multidimensionale)
  Utilizzare la finestra di dialogo **Proprietà database** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per impostare le proprietà di un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Per visualizzare la finestra di dialogo **Proprietà database** è possibile fare clic con il pulsante destro del mouse su un database in Esplora oggetti e scegliere **Proprietà**.  
  
## <a name="options"></a>Opzioni  
  
|Nome|Definizione|  
|----------|----------------|  
|**Name**|Consente di modificare il nome del database.|  
|**ID**|Consente di visualizzare l'identificatore del database.|  
|**Descrizione**|Consente di modificare la descrizione del database.|  
|**Timestamp creazione**|Consente di visualizzare la data e l'ora di creazione del database.|  
|**Ultimo aggiornamento schema**|Consente di visualizzare la data e l'ora dell'ultimo aggiornamento dei metadati del database.|  
|**Ultimo aggiornamento**|Consente di visualizzare la data e l'ora dell'ultimo aggiornamento dei dati del database.|  
|**Impostazioni di rappresentazione origine dati**|Consente di selezionare le informazioni di rappresentazione utilizzate dal database per la connessione e l'interazione con le origini dei dati contenute nel database. I valori validi sono i seguenti:<br /><br /> **ImpersonateAccount** (usare un nome utente e una password specifici di Windows).<br /><br /> **ImpersonateService** (usare l'account del servizio).<br /><br /> **ImpersonateCurrentUser** (usare le credenziali dell'utente corrente).<br /><br /> **Default** (usare l'account del servizio per le operazioni MOLAP e l'utente corrente per il data mining).<br /><br /> Sebbene sia possibile definire le impostazioni di rappresentazione dell'origine dati al livello del database, questa operazione influirebbe unicamente sulle origini dati per cui è stato specificato **Eredita** per le impostazioni della rappresentazione. Le impostazioni di rappresentazione specificate direttamente sull'origine dati eseguiranno sempre l'override delle impostazioni specificate al livello del database.<br /><br /> Quando si sceglie un'opzione di rappresentazione, considerare i tipi di operazioni che dovranno essere supportati. Alcune operazioni, ad esempio l'elaborazione, non possono essere eseguite da|  
|**Ultima elaborazione**|Consente di visualizzare la data e l'ora dell'ultima elaborazione del database.|  
|**Dimensioni stimate**|Consente di visualizzare le dimensioni stimate del database.|  
|**Percorso di archiviazione**|Specifica la posizione del database. Se il database si trova nella directory dati predefinita, questo valore sarà vuoto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Database modelli multidimensionali &#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
