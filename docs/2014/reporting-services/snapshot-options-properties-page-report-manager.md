---
title: Opzioni snapshot pagina delle proprietà (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f6641f59-5267-4f57-8957-63b93d1a9679
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7a73f3be75a7f0cadf633943aeafffb7217d8e29
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101155"
---
# <a name="snapshot-options-properties-page-report-manager"></a>Pagina delle proprietà Opzioni snapshot (Gestione report)
  Utilizzare la pagina delle proprietà Opzioni snapshot per pianificare gli snapshot del report da aggiungere alla cronologia del report e impostare limiti per il numero di snapshot del report archiviati nella cronologia.  
  
> [!NOTE]  
>  Questa funzionalità non è disponibile in ogni edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [altri servizi di Database](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md#Add_DBServices).  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
### <a name="to-open-the-snapshot-options-properties-page-for-a-report"></a>Per aprire la pagina delle proprietà Opzioni snapshot per un report  
  
1.  Aprire Gestione report, quindi individuare il report per il quale si desidera configurare le proprietà dello snapshot del report.  
  
2.  Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa. Verrà visualizzata la pagina delle proprietà Generale per il report.  
  
4.  Selezionare la scheda **Opzioni snapshot** .  
  
## <a name="options"></a>Opzioni  
 **Consenti creazione manuale della cronologia del report**  
 Selezionare questa casella di controllo per aggiungere snapshot alla cronologia del report, se necessario. Se si seleziona questa casella di controllo, nella pagina Cronologia verrà visualizzato il pulsante **Nuovo snapshot** .  
  
 **Store tutti gli snapshot di esecuzione di report nella cronologia del report**  
 Selezionare questa casella di controllo per copiare nella cronologia gli snapshot del report generati in base alle proprietà di esecuzione del report. È possibile impostare le proprietà di esecuzione del report in modo da eseguire un report da uno snapshot generato. L'impostazione di questa proprietà della cronologia consente di mantenere una registrazione di tutti gli snapshot del report generati nel tempo tramite l'inserimento di copie degli snapshot nella cronologia del report.  
  
 **Usa la pianificazione seguente per aggiungere snapshot alla cronologia del report**  
 Selezionare questa casella di controllo per aggiungere gli snapshot alla cronologia del report in base a una pianificazione prestabilita. È possibile creare una pianificazione utilizzata esclusivamente a questo scopo oppure selezionare una pianificazione condivisa predefinita, nel caso sia disponibile una pianificazione pronta appropriata.  
  
 **Selezionare il numero di snapshot da mantenere**  
 Selezionare una delle opzioni indicate di seguito per stabilire il numero di report da mantenere nella cronologia. Le impostazioni di cronologia del report possono variare per ogni report.  
  
-   Selezionare **Usa impostazione predefinita** per utilizzare l'impostazione predefinita. L'amministratore del server di report gestisce un'impostazione globale per l'archiviazione della cronologia dei report. Se si seleziona questa opzione, il numero di snapshot da mantenere corrisponde a quello impostato dall'amministratore.  
  
-   Selezionare **Nessun limite per il numero di snapshot archiviabili nella cronologia** per conservare tutti gli snapshot della cronologia del report. Per mantenere ridotte le dimensioni della cronologia del report sarà necessario eliminare manualmente gli snapshot non più necessari.  
  
-   Selezionare **Numero massimo di copie della cronologia** per conservare un numero specifico di snapshot. Raggiunto tale limite, le copie meno recenti vengono rimosse dalla cronologia del report per fare spazio alle copie più recenti.  
  
 La cronologia del report viene archiviata nel database del server di report. Se vi sono report di grandi dimensioni o numerosi report per i quali si desidera conservare la cronologia, limitare la quantità di cronologia del report per semplificare la gestione dei requisiti di spazio su disco del database del server di report.  
  
 **Applica**  
 Fare clic per salvare le modifiche.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere uno snapshot alla cronologia del report &#40;Gestione report&#41;](report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Creare, modificare ed eliminare snapshot nella cronologia dei report](report-server/create-modify-and-delete-snapshots-in-report-history.md)   
 [Guida sensibile al contesto di Gestione report](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
