---
title: Definire una variabile di stato | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 45d66152-883a-49a7-a877-2e8ab45f8f79
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 64f1b991d0978e45cbfa9dbf19ba796cc824bf5c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292933"
---
# <a name="define-a-state-variable"></a>Definire una variabile di stato

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  In questa procedura viene descritto come definire una variabile del pacchetto in cui è archiviato lo stato CDC.  
  
 La variabile di stato CDC viene caricata, inizializzata e aggiornata tramite l'attività di controllo CDC e viene utilizzata dal componente flusso di dati dell'origine CDC per determinare l'intervallo di elaborazione corrente per i record delle modifiche. È possibile definire la variabile di stato CDC in qualsiasi contenitore comune all'attività di controllo CDC e all'origine CDC. Ciò può avvenire a livello di pacchetto, ma anche in altri contenitori, ad esempio un contenitore Ciclo.  
  
 Non è consigliabile modificare manualmente il valore della variabile di stato CDC, tuttavia questa operazione può risultare utile per comprenderne il contenuto.  
  
 Nella tabella seguente viene fornita una descrizione di alto livello dei componenti del valore della variabile di stato CDC.  
  
|Componente|Descrizione|  
|---------------|-----------------|  
|**\<state-name>**|Si tratta del nome dello stato CDC corrente.|  
|**CS**|Viene contrassegnato il punto di inizio dell'intervallo di elaborazione corrente (inizio corrente).|  
|**\<cs-lsn>**|Si tratta dell'ultimo numero di sequenza del file di log (LSN) elaborato nell'esecuzione CDC precedente.|  
|**CE**|Viene contrassegnato il punto di fine dell'intervallo di elaborazione corrente (fine corrente). La presenza del componente CE nello stato CDC indica che un pacchetto CDC è attualmente in fase di elaborazione o che si è verificato un errore di esecuzione di un pacchetto CDC prima del completamento dell'elaborazione dell'intervallo di elaborazione CDC.|  
|**\<ce-lsn>**|Si tratta dell'ultimo LSN da elaborare nell'esecuzione CDC corrente. Viene sempre presupposto che l'ultimo numero di sequenza da elaborare sia il valore massimo (0xFFF...).|  
|**IR**|Viene contrassegnato l'intervallo di elaborazione iniziale.|  
|**\<ir-start>**|Si tratta di un numero LSN di una modifica appena prima dell'avvio del caricamento iniziale.|  
|**\<ir-end>**|Si tratta di un numero LSN di una modifica appena dopo il completamento del caricamento iniziale.|  
|**TS**|Viene contrassegnato il timestamp per l'ultimo aggiornamento dello stato CDC.|  
|**\<timestamp>**|Si tratta di una rappresentazione decimale della proprietà System.DateTime.UtcNow a 64 bit.|  
|**ER**|Viene visualizzato quando si verifica un errore durante l'esecuzione dell'ultima operazione ed è inclusa una breve descrizione della causa dell'errore. Se il componente è presente, viene sempre visualizzato per ultimo.|  
|**\<short-error-text>**|Si tratta della breve descrizione dell'errore.|  
  
 I numeri LSN e di sequenza sono tutti codificati come stringa esadecimale fino a un massimo di 20 cifre che rappresentano il valore LSN di Binary(10).  
  
 Nella tabella seguente vengono descritti i possibili valori dello stato CDC.  
  
|State|Descrizione|  
|-----------|-----------------|  
|(INITIAL)|Si tratta dello stato iniziale prima dell'esecuzione di qualsiasi pacchetto nel gruppo CDC corrente. È anche lo stato quando lo stato CDC è vuoto.|  
|ILSTART (Initial Load Started)|Si tratta dello stato all'avvio del pacchetto di caricamento iniziale, dopo la chiamata dell'operazione **MarkInitialLoadStart** all'attività di controllo CDC.|  
|ILEND (Initial Load Ended)|Si tratta dello stato al corretto completamento del pacchetto di caricamento iniziale, dopo la chiamata dell'operazione **MarkInitialLoadEnd** all'attività di controllo CDC.|  
|ILUPDATE (Initial Load Update)|Si tratta dello stato durante l'esecuzione del pacchetto di aggiornamento Trickle-Feed in seguito al caricamento iniziale, mentre l'elaborazione dell'intervallo di elaborazione iniziale è ancora in corso. Si verifica dopo la chiamata dell'operazione **GetProcessingRange** all'attività di controllo CDC.<br /><br /> Se si utilizza la colonna __$reprocessing, viene impostato su 1 per indicare che a livello di destinazione è possibile che le righe siano già in corso di rielaborazione.|  
|TFEND (Trickle-Feed Update Ended)|Si tratta dello stato previsto per le esecuzioni CDC normali. Indica che l'esecuzione precedente è stata completata e che è possibile avviare una nuova esecuzione con un nuovo intervallo di elaborazione.|  
|TFSTART|Si tratta dello stato durante un'esecuzione non iniziale del pacchetto di aggiornamento Trickle-Feed, dopo la chiamata dell'operazione **GetProcessingRange** all'attività di controllo CDC.<br /><br /> Indica che un'esecuzione CDC normale è stata avviata in maniera pulita, ma non è stata o non è ancora,terminata (**MarkProcessedRange**).|  
|TFREDO (Reprocessing Trickle-Feed Updates)|Si tratta dello stato di **GetProcessingRange** che si verifica dopo TFSTART. Indica che l'esecuzione precedente non è stata completata correttamente.<br /><br /> Se si utilizza la colonna __$reprocessing, viene impostato su 1 per indicare che a livello di destinazione è possibile che le righe siano già in corso di rielaborazione.|  
|ERROR|Il gruppo CDC si trova in uno stato ERROR.|  
  
 Di seguito sono riportati esempi di valori della variabile di stato CDC.  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   TFEND/CS/0x0000025B000001BC0003/TS/2011-07-17T12:05:58.1001145/  
  
-   TFSTART/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:43.9344900/  
  
-   TFREDO/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:59.5544900/  
  
### <a name="to-define-a-cdc-state-variable"></a>Per definire una variabile di stato CDC  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]aprire il pacchetto di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] contenente il flusso CDC in cui è necessario definire la variabile.  
  
2.  Fare clic sulla scheda **Esplora pacchetti** e aggiungere una nuova variabile.  
  
3.  Assegnare un nome alla variabile in modo da poterla riconoscere come variabile di stato.  
  
4.  Assegnare alla variabile un tipo di dati **String** .  
  
 Non assegnare alla variabile un valore come parte della definizione. Il valore deve essere impostato tramite l'attività di controllo CDC.  
  
 Se si intende utilizzare l'attività di controllo CDC con **Automatic State Persistence**, la variabile di stato CDC verrà letta dalla tabella degli stati del database specificata e verrà riaggiornata nella stessa tabella quando cambia il relativo valore. Per ulteriori informazioni sulla tabella degli stati, vedere [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md)e [CDC Control Task Editor](../../integration-services/control-flow/cdc-control-task-editor.md).  
  
 Se non si utilizza l'attività di controllo CDC con Automatic State Persistence, è necessario caricare il valore della variabile dall'archivio permanente in cui sono stati salvati i relativi valori all'ultima esecuzione del pacchetto e riscriverlo nell'archivio permanente in cui è stata completata l'elaborazione dell'intervallo di elaborazione corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività di controllo CDC](../../integration-services/control-flow/cdc-control-task.md)   
 [Editor attività Controllo CDC](../../integration-services/control-flow/cdc-control-task-editor.md)  
  
  
