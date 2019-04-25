---
title: Visualizzare la Data dell'aggiornamento della cronologia (Power Pivot per SharePoint) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 355ade7f4c90b595356efc5d39c2fa7cf587b11b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62509943"
---
# <a name="view-data-refresh-history-power-pivot-for-sharepoint"></a>Visualizzare la cronologia dell'aggiornamento dati (Power Pivot per SharePoint)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La cronologia dell'aggiornamento dati è un record di tutte le attività di aggiornamento dei dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in una cartella di lavoro di Excel. Le operazioni di aggiornamento dati vengono eseguite in un'istanza del server Analysis Services di una farm di SharePoint in base a una pianificazione fornita dall'utente. Per impostazione predefinita, la cronologia dell'aggiornamento dati viene mantenuta per un anno. L'amministratore di una farm può tuttavia specificare criteri di memorizzazione diversi per la cronologia relativa all'utilizzo e agli eventi, in modo da stabilire la durata di mantenimento in memoria dei record dell'aggiornamento dati.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **Contenuto dell'argomento:**  
  
 [Prerequisiti](#prereq)  
  
 [Visualizzare la cronologia dell'aggiornamento dati per una singola cartella di lavoro](#viewhistory)  
  
 [Visualizzare la cronologia dell'aggiornamento dati per tutte le cartelle di lavoro](#viewITOps)  
  
 [Utilizzare le informazioni sulla cronologia](#pageelements)  
  
##  <a name="prereq"></a> Prerequisiti  
 È necessario disporre di autorizzazioni di collaborazione o superiori per visualizzare la cronologia dell'aggiornamento dati.  
  
 È necessario avere abilitato e pianificato l'aggiornamento dei dati in una cartella di lavoro contenente dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Se l'aggiornamento dei dati non è stato pianificato, verrà visualizzata la pagina di definizione della pianificazione anziché le informazioni relative alla cronologia.  
  
##  <a name="viewhistory"></a> Visualizzare la cronologia dell'aggiornamento dati per una singola cartella di lavoro  
  
1.  In un sito di SharePoint aprire la raccolta in cui è inclusa una cartella di lavoro di Excel contenente dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
     Non viene visualizzato alcun indicatore che consenta di identificare le cartelle di lavoro di una raccolta di SharePoint contenenti dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . È necessario sapere in anticipo in quale cartella di lavoro sono inclusi dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] aggiornabili.  
  
2.  Selezionare la cartella di lavoro, quindi fare clic sulla freccia GIÙ visualizzata sul lato destro.  
  
3.  Selezionare **Gestisci aggiornamento dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**.  
  
 Viene visualizzata la pagina della cronologia in cui è disponibile un record completo per tutte le attività di aggiornamento relative ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nella cartella di lavoro di Excel corrente.  
  
##  <a name="viewITOps"></a> Visualizzare la cronologia dell'aggiornamento dati per tutte le cartelle di lavoro  
 Usando il dashboard di gestione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in Amministrazione centrale, gli amministratori della farm e gli amministratori dell'applicazione di servizio possono ottenere una vista completa della cronologia e dello stato di aggiornamento dei dati per tutte le cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Per altre informazioni, vedere [Power Pivot Management Dashboard and Usage Data](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
##  <a name="pageelements"></a> Utilizzare le informazioni sulla cronologia  
 Nella pagina della cronologia dell'aggiornamento dati vengono fornite informazioni dettagliate sulle singole operazioni di aggiornamento. È possibile utilizzare le informazioni contenute in questa pagina per verificare se l'aggiornamento è stato eseguito o il motivo per cui non è stato completato correttamente.  
  
|Elemento|Descrizione|  
|----------|-----------------|  
|Nome|Specifica il nome di file della cartella di lavoro di Excel in cui sono contenuti i dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
|Stato corrente|I valori disponibili sono **Pianificato**, **Aggiornamento in corso**, **Operazione completata**o **Operazione non riuscita**.<br /><br /> Il valore**Pianificato** viene visualizzato quando si crea per la prima volta la pianificazione. Dopo la prima esecuzione dell'aggiornamento dei dati, questo messaggio di stato non viene più visualizzato.<br /><br /> **Aggiornamento in corso** indica che è in corso l'aggiornamento dei dati. Una richiesta si trova nella coda dei processi o è in esecuzione nel server.<br /><br /> **Operazione completata** indica che l'ultima operazione di aggiornamento dei dati è stata completata e la cartella di lavoro aggiornata viene nuovamente archiviata nella raccolta di SharePoint.<br /><br /> **Operazione non riuscita** indica che l'ultima operazione di aggiornamento dei dati non è stata completata. I dati aggiornati non sono stati salvati. Nella cartella di lavoro sono inclusi gli stessi dati presenti prima dell'inizio dell'aggiornamento.|  
|Ultimo aggiornamento riuscito|Consente di specificare la data in cui l'ultimo aggiornamento dei dati è stato completato correttamente.|  
|Prossimo aggiornamento pianificazione|Consente di specificare la data in cui è previsto il prossimo aggiornamento dei dati in base alla pianificazione.<br /><br /> Il collegamento **Configura pianificazione** reindirizza l'utente alla pagina di definizione della pianificazione. Se la cartella di lavoro contiene le autorizzazioni di collaborazione, è possibile fare clic sul collegamento per visualizzare e modificare le informazioni sulla pianificazione che regolano l'aggiornamento automatico dei dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nella cartella di lavoro.|  
|Started|All'interno della sezione relativa ai dettagli della cronologia, **Avvio eseguito** indica il tempo di elaborazione effettivo. Il tempo di elaborazione effettivo potrebbe essere diverso da quello pianificato. L'elaborazione inizierà quando è disponibile memoria sufficiente sul server. Se il server è molto occupato, l'elaborazione potrebbe iniziare diverse ore dopo l'ora di inizio specificata.|  
|Operazione completata|All'interno della sezione relativa ai dettagli della cronologia, **Completato** indica il momento in cui l'operazione di aggiornamento dei dati è stata completata. Sono specificate la data e l'ora in cui la cartella di lavoro è stata nuovamente archiviata nella raccolta.<br /><br /> Se l'aggiornamento dei dati ha esito negativo, la causa dell'errore viene illustrata in uno o più i messaggi di errore. È possibile espandere ogni record per visualizzare i dettagli sullo stato. Ogni origine dati viene elencata singolarmente, accanto ai messaggi relativi all'esito positivo o negativo nel quali viene spiegato il motivo per cui l'aggiornamento dei dati non è stato completato.|  
|Time|Viene fornito il tempo totale dall'avvio dell'aggiornamento dei dati fino al completamento.|  
|Stato|Viene fornito un record cronologico relativo all'esito positivo o negativo di un'operazione di aggiornamento.|  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare la raccolta dati di utilizzo per PowerPivot per SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [Pianificare un aggiornamento dati (Power Pivot per SharePoint)](http://msdn.microsoft.com/8571208f-6aae-4058-83c6-9f916f5e2f9b)   
 [Aggiornamento dati Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh.md)  
  
  
