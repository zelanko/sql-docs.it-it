---
title: Editor attività Profiling dati (pagina Generale) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataprofilingtask.general.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: eec15906-d757-4079-b2f6-aca4e52b3b4c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8462f85dc6c804020f12b9bc989d683c5a4ad0ba
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58385353"
---
# <a name="data-profiling-task-editor-general-page"></a>Editor attività Profiling dati (pagina Generale)
  Usare la pagina **Generale** di **Editor attività Profiling dati** per configurare le opzioni seguenti:  
  
-   Specificare la destinazione per l'output del profilo.  
  
-   Utilizzare le impostazioni predefinite per semplificare l'attività di profiling di una singola tabella o vista.  
  
 Per altre informazioni sull'uso dell'attività Profiling dati, vedere [Impostazione dell'attività Profiling dati](data-profiling-task.md). Per altre informazioni sull'uso del Visualizzatore profilo dati per analizzare l'output dell'attività Profiling dati, vedere [Visualizzatore profilo dati](data-profile-viewer.md).  
  
 **Per aprire la pagina Generale in Editor attività Profiling dati**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] contenente l'attività Profiling dati.  
  
2.  Nella scheda **Flusso di controllo** fare doppio clic sull'attività Profiling dati.  
  
3.  In **Editor attività Profiling dati**fare clic su **Generale**.  
  
## <a name="data-profiling-options"></a>Opzioni di profiling dei dati  
 **Timeout**  
 Specifica il numero di secondi dopo il quale attivare il timeout dell'attività Profiling dati e arrestarne l'esecuzione. Il valore predefinito è 0, che non specifica alcun timeout.  
  
## <a name="destination-options"></a>Opzioni destinazione  
  
> [!IMPORTANT]  
>  Il file di output potrebbe contenere dati sensibili sul database e i dati inclusi nel database. Per suggerimenti su come rendere più sicuro questo file, vedere [Accesso ai file utilizzati dai pacchetti](../access-to-files-used-by-packages.md).  
  
 **DestinationType**  
 Consente di specificare se salvare l'output del profilo dei dati in un file o una variabile:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**FileConnection**|Consente di salvare l'output del profilo in un file nel percorso specificato in una gestione connessione file.<br /><br /> Nota: Si specifica la gestione connessione File da usare nel **destinazione** opzione.|  
|**Variabile**|Consente di salvare l'output del profilo in una variabile del pacchetto.<br /><br /> Nota: È possibile specificare la variabile di pacchetto da utilizzare nel **destinazione** opzione.|  
  
 **Destinazione**  
 Consente di specificare la gestione connessione file o la variabile del pacchetto contenente l'output del profilo dei dati:  
  
-   Se l'opzione **DestinationType** è impostata su **FileConnection**, l'opzione **Destination** visualizza le gestioni connessione file disponibili. Selezionare una delle gestioni connessione oppure fare clic su \<Nuova connessione file> per creare una nuova gestione connessione file.  
  
-   Se l'opzione **DestinationType** è impostata su **Variable**, l'opzione **Destination** visualizza le variabili del pacchetto disponibili nell'elenco **Destination** . Selezionare una delle variabili oppure fare clic su \<Nuova variabile> per crearne una nuova.  
  
 **OverwriteDestination**  
 Consente di specificare se sovrascrivere il file di output, se presente. Il valore predefinito è **False**. Il valore di questa proprietà viene utilizzato solo quando l'opzione DestinationType è impostata su FileConnection. Quando l'opzione DestinationType è impostata su Variable, l'attività sovrascrive sempre il valore precedente della variabile.  
  
> [!IMPORTANT]  
>  Se si tenta di eseguire l'attività Profiling dati più di una volta senza modificare il nome del file di output o impostare il valore della proprietà **OverwriteDestination** su **True**, l'attività restituirà un errore e un messaggio indicante che il file di output è già presente.  
  
## <a name="other-options"></a>Altre opzioni  
 **Profilo rapido**  
 Consente di visualizzare l'opzione **Form profilo rapido singola tabella**. Questo form semplifica l'attività di profiling di una singola tabella o vista tramite le impostazioni predefinite. Per altre informazioni, vedere [Form profilo rapido singola tabella &#40;Attività Profiling dati&#41;](single-table-quick-profile-form-data-profiling-task.md).  
  
 **Apri Visualizzatore profilo**  
 Consente di aprire il Visualizzatore profilo dati. Il Visualizzatore profilo dati autonomo visualizza l'output del profilo dei dati dall'attività Profiling dati. È possibile visualizzare l'output del profilo dei dati dopo avere eseguito l'attività Profiling dati nel pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e aver calcolato i profili dati.  
  
> [!NOTE]  
>  È anche possibile aprire il Visualizzatore profilo dati eseguendo DataProfileViewer.exe nella cartella *\<unità>*:\Programmi (x86) | Programmi\Microsoft SQL Server\110\DTS\Binn.  
  
## <a name="see-also"></a>Vedere anche  
 [Form profilo rapido singola tabella &#40;Attività Profiling dati&#41;](single-table-quick-profile-form-data-profiling-task.md)   
 [Editor attività Profiling dati &#40;pagina Richieste profilo&#41;](data-profiling-task-editor-profile-requests-page.md)  
  
  
