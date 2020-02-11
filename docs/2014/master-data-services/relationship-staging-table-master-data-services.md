---
title: Tabella di gestione temporanea delle relazioni (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- relationships staging table [Master Data Services]
- database [Master Data Services], relationships table
ms.assetid: e19b6002-67bd-4e7d-9f19-ecb455522b1a
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3b5cc194306a4baecb2c5fa5478bf4733d1386af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67284985"
---
# <a name="relationship-staging-table-master-data-services"></a>Tabella di gestione temporanea delle relazioni (Master Data Services)
  Usare la tabella di staging delle relazioni nel database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] per modificare il percorso dei membri in una gerarchia esplicita, in base alla relazione esistente tra i membri.  
  
##  <a name="TableColumns"></a>Colonne della tabella  
 Nella seguente tabella viene illustrato il motivo per cui viene utilizzato ogni campo della tabella di staging Relazione.  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|**ID**|Un identificatore assegnato automaticamente. Non immettere un valore in questo campo. Se il batch non è stato elaborato, questo campo è vuoto.|  
|**RelationshipType**<br /><br /> Obbligatoria|Il tipo di relazione impostata. Valori possibili:<br /><br /> **1**:P adre<br /><br /> **2**: elemento di pari livello (allo stesso livello)|  
|**ImportStatus_ID**<br /><br /> Obbligatoria|Lo stato del processo di importazione. Valori possibili:<br /><br /> **0**, specificato per indicare che il record è pronto per la gestione temporanea.<br /><br /> **1**, assegnato automaticamente e indica che il processo di gestione temporanea del record ha avuto esito positivo.<br /><br /> **2**, assegnato automaticamente e indica che il processo di gestione temporanea del record non è riuscito.|  
|**Batch_ID**<br /><br /> Richiesto solo dal servizio Web|Un identificatore assegnato automaticamente che raggruppa i record per la gestione temporanea. A tutti i membri nel batch viene assegnato questo identificatore, visualizzato nella colonna [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ID **dell'interfaccia utente di** .<br /><br /> Se il batch non è stato elaborato, questo campo è vuoto.|  
|**BatchTag**<br /><br /> Richiesto, salvo che dal servizio Web|Un nome univoco per il batch, composto da un massimo di 50 caratteri.|  
|**HierarchyName**<br /><br /> Obbligatoria|Il nome della gerarchia esplicita. Ogni membro consolidato può appartenere solo ad un'unica gerarchia.|  
|**ParentCode**<br /><br /> Obbligatoria|Per le relazioni padre-figlio, il codice del membro consolidato che sarà il padre della foglia figlio o del membro consolidato.<br /><br /> Per le relazioni di pari livello, il codice di uno degli elementi di pari livello.|  
|**ChildCode**<br /><br /> Obbligatoria|Per le relazioni padre-figlio, il codice del membro consolidato o foglia che sarà il figlio.<br /><br /> Per le relazioni di pari livello, il codice di uno degli elementi di pari livello.|  
|**Ordinamento**<br /><br /> Facoltativo|Un valore intero che indica l'ordine del membro in relazione agli altri membri sottostanti l'elemento padre. Ciascun membro figlio deve disporre di un identificatore univoco.|  
|**ErrorCode**|Visualizza un codice di errore. Per tutti i record con **ImportStatus_ID** di **2**, vedere [Errori del processo di gestione temporanea &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Spostare membri di gerarchie esplicite tramite il processo di gestione temporanea &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)   
 [Importazione dati &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [Visualizzare gli errori che si verificano durante il processo di gestione temporanea &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)   
 [Errori del processo di gestione temporanea &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md)  
  
  
