---
title: Opzioni di elaborazione pagina delle proprietà (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 28f07c70-7132-4d15-9505-4fdf31dc9cc0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 524fcaea873128ea4bde6ccdc213a29ec31cc77d
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59939157"
---
# <a name="processing-options-properties-page-report-manager"></a>Pagina delle proprietà Opzioni di elaborazione (Gestione report)
  Utilizzare la pagina delle proprietà Opzioni di elaborazione per impostare le proprietà di esecuzione del report per il report selezionato. Le opzioni disponibili in questa pagina consentono di impostare la tempistica di elaborazione dei dati per il report. È possibile impostare queste opzioni per recuperare i dati di un report durante gli orari con minore attività. Nel caso di un report utilizzato frequentemente, è possibile impostare la memorizzazione temporanea di copie del report nella cache per evitare attese se più utenti accedono allo stesso report a intervalli di pochi minuti l'uno dall'altro.  
  
> [!NOTE]  
>  La cronologia dei report, gli snapshot delle funzionalità di esecuzione e memorizzazione nella cache non sono disponibili in ogni edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-processing-options-properties-page"></a>Per aprire la pagina delle proprietà Opzioni di elaborazione  
  
1.  Aprire Gestione report e individuare il report per il quale si desidera impostare le proprietà di elaborazione.  
  
2.  Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa. Verrà visualizzata la pagina delle proprietà Generale per il report.  
  
4.  Selezionare la scheda **Opzioni di elaborazione** .  
  
## <a name="options"></a>Opzioni  
 **Eseguire sempre questo report con i dati più recenti**  
 Selezionare questa opzione se si desidera recuperare i dati del report quando il report viene selezionato dall'utente. Se nella cache è disponibile una copia del report, tale copia viene restituita all'utente. In caso contrario, il recupero dei dati e il rendering vengono eseguiti quando un utente seleziona il report.  
  
 Selezionare **Non memorizzare nella cache copie temporanee del report** per eseguire sempre il report con i dati più recenti. Ogni utente che apre il report attiva una query sull'origine dati contenente i dati utilizzati nel report.  
  
 Selezionare **Memorizza nella cache una copia temporanea del report**per memorizzare una copia temporanea del report in una cache quando il report viene aperto per la prima volta da un utente. Gli utenti che eseguono successivamente il report durante il periodo di memorizzazione nella cache riceveranno la copia del report memorizzata nella cache. La memorizzazione nella cache consente in genere di migliorare le prestazioni in quanto il report viene restituito dalla cache anziché essere rielaborato.  
  
 Per i report memorizzati nella cache deve essere prevista una scadenza. Specificare il numero di minuti per il salvataggio della copia memorizzata nella cache del report. Dopo la scadenza, la copia temporanea non viene più restituita dalla cache. Alla successiva apertura del report da parte di un utente, il server di report rielabora il report e memorizza nella cache una copia del report aggiornato.  
  
 È inoltre possibile impostare una pianificazione per la scadenza di un report memorizzato nella cache utilizzando una frequenza diversa dai minuti. Per impostare una scadenza giornaliera per un report nella cache, ad esempio, è possibile selezionare un'ora notturna specifica per la scadenza della copia.  
  
 **Eseguire il rendering di report da uno snapshot dell'esecuzione report**  
 Selezionare questa opzione per recuperare un report archiviato come snapshot in base alla pianificazione impostata. Quando si sceglie questa opzione, è possibile pianificare l'elaborazione dei dati in modo che venga eseguita negli orari con minore attività. Diversamente dalle copie memorizzate nella cache che vengono create all'apertura del report da parte di un utente, gli snapshot vengono creati e successivamente aggiornati in base a una pianificazione. Per gli snapshot non è prevista una scadenza, ovvero rimangono attivi fino a quando non vengono sostituiti con versioni più recenti.  
  
 Gli snapshot generati in base alle impostazioni di esecuzione del report hanno le stesse caratteristiche degli snapshot della cronologia dei report. La differenza è rappresentata dal fatto che esiste un solo snapshot dell'esecuzione del report mentre possono esistere potenzialmente molti snapshot della cronologia dei report. È possibile accedere agli snapshot della cronologia dei report dalla pagina Cronologia del report, nella quale vengono archiviate numerose istanze di un report, nelle versioni esistenti in diversi momenti nel tempo. È invece possibile accedere agli snapshot dell'esecuzione del report dalle cartelle, nello stesso modo in cui si accede ai report live. Per gli snapshot di esecuzione del report non sono previsti indicatori visivi particolari per segnalare agli utenti che il report è uno snapshot.  
  
 Selezionare l'opzione correlata di **Crea uno snapshot del report quando viene scelto il pulsante Applica in questa pagina** per creare uno snapshot del report quando si fa clic sul pulsante Applica. In questo modo verrà generato immediatamente uno snapshot del report per renderlo disponibile prima dell'ora di inizio pianificata.  
  
 **Timeout esecuzione report**  
 Consente di specificare se si desidera impostare un timeout per l'elaborazione del report dopo un numero specifico di secondi. Se si seleziona l'impostazione predefinita, per questo report verrà utilizzata l'impostazione di timeout selezionata nella pagina Impostazioni sito.  
  
 Tale valore viene applicato all'elaborazione dei report in un server di report. L'impostazione non ha effetto sull'elaborazione dei dati nel server di database che fornisce i dati per il report. Il valore specificato deve tuttavia essere sufficiente per consentire il completamento dell'elaborazione sia dei dati che del report. Il conteggio dell'elaborazione del report inizia nel momento in cui viene selezionato il report e termina all'apertura del report.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare proprietà di elaborazione dei report](report-server/set-report-processing-properties.md)   
 [Memorizzazione dei report nella cache &#40;SSRS&#41;](report-server/caching-reports-ssrs.md)   
 [Create, Modify, and Delete Schedules](subscriptions/create-modify-and-delete-schedules.md)   
 [Guida sensibile al contesto di Gestione report](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
