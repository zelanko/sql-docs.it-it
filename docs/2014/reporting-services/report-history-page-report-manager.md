---
title: Report pagina della cronologia (gestione Report) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 0b0841e031ee1a98f4f678406f790996a709e90f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66104476"
---
# <a name="report-history-page-report-manager"></a>Pagina Cronologia report (Gestione report)

La pagina Cronologia report consente di visualizzare gli snapshot del report generati e archiviati nel corso del tempo. A seconda delle opzioni impostate nel server di report, è possibile che la cronologia del report includa solo gli snapshot più recenti.  
  

La cronologia del report viene sempre visualizzata nel contesto del report a cui si riferisce, ovvero non è possibile visualizzare la cronologia di tutti i report in un server di report in un'unica posizione.  
  
Per generare la cronologia, è necessario che il report possa essere eseguito in modo automatico, ovvero il report deve utilizzare credenziali archiviate e i report con parametri devono includere valori predefiniti per tutti i parametri. È possibile generare la cronologia del report manualmente o come operazione pianificata. Le proprietà della cronologia del report determinano i metodi di creazione consentiti.  
  
È possibile fare clic su uno snapshot della cronologia del report per visualizzarlo. L'unico elemento distintivo degli snapshot visualizzati nella cronologia del report è rappresentato dalla data e ora di creazione. Non sono disponibili indicatori visivi per distinguere gli snapshot generati tramite una pianificazione o un'operazione manuale.  
  
> [!NOTE]  
>  Questa funzionalità non è disponibile in ogni edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
### <a name="to-open-the-report-history-page"></a>Per aprire la pagina Cronologia report  
  
1.  Aprire Gestione report e individuare il report per il quale si desidera visualizzare gli snapshot del report.  
  
2.  Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
3.  Nel menu a discesa fare clic su **Visualizza cronologia report**.  
  
## <a name="options"></a>Opzioni  
 **Elimina**  
 Fare clic per eliminare uno o più snapshot. Prima di fare clic su **Elimina**selezionare la casella di controllo accanto allo snapshot che si desidera eliminare.  
  
 **Nuovo Snapshot**  
 Fare clic per aggiungere uno snapshot alla cronologia del report. Questo pulsante è disponibile se si seleziona l'opzione **Consenti creazione manuale della cronologia** nella pagina delle proprietà Cronologia del report.  
  
 **Ultima esecuzione**  
 Visualizza data e ora di creazione dello snapshot. Fare clic su una descrizione per visualizzare uno snapshot specifico.  
  
 **Dimensione**  
 Visualizza la dimensione della definizione e dei dati del report. Questo valore indica lo spazio occupato nel database del server di report dalla definizione e dai dati del report. Le dimensioni del report visualizzabile, che include elementi di formattazione, sono effettivamente più grandi. Le dimensioni totali, indicate tra parentesi, rappresentano la somma delle dimensioni di tutti gli snapshot presenti nella cronologia del report per il report corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare o eliminare la cronologia del Report &#40;gestione Report&#41;](../../2014/reporting-services/view-or-delete-report-history-report-manager.md)   
 [Aggiungere uno snapshot alla cronologia del report &#40;Gestione report&#41;](report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Pagina delle proprietà Generale, Report &#40;Gestione report&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [Guida F1 di gestione report](../../2014/reporting-services/report-manager-f1-help.md)   
 [Pagina delle proprietà Opzioni snapshot &#40;gestione Report&#41;](../../2014/reporting-services/snapshot-options-properties-page-report-manager.md)