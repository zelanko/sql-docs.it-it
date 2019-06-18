---
title: Impostare le opzioni di controllo codice sorgente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Source_Control.Visual_SourceSafe
- VS.ToolsOptionsPages.Source_Control.General
- VS.ToolsOptionsPages.Source_Control.Environment
helpviewer_keywords:
- source controls [SQL Server Management Studio], options
ms.assetid: b2c6ca00-46f0-4f86-b067-07bae779c147
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0a654932689785d96aaff049551faf19494c311a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62843735"
---
# <a name="set-source-control-options"></a>Impostare le opzioni di controllo del codice sorgente
  Per utilizzare le caratteristiche di controllo del codice sorgente incorporate in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], è necessario configurare le relative opzioni per i diversi ambienti di lavoro.  
  
 Per configurare le opzioni di controllo di origine, utilizzare il **opzioni** finestra di dialogo per configurare uno o più ruoli del controllo codice sorgente. Un ruolo è una descrizione generale dell'impostazione utilizzata per [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e delle opzioni di controllo del codice sorgente associate a questa impostazione.  
  
 Ad esempio, uno sviluppatore di database indipendente generalmente non crea conflitti con altri utenti mantenendo file estratti dopo averli archiviati. Di conseguenza, in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] viene definito un ruolo Sviluppatore Indipendente. Per questo ruolo [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] seleziona automaticamente il **Mantieni gli elementi estratti durante l'archiviazione** opzione.  
  
 Poiché i ruoli possono essere definiti e personalizzati, è possibile lavorare con impostazioni di sviluppo diverse senza riconfigurare completamente il controllo del codice sorgente ogni volta che si passa da un'impostazione all'altra.  
  
### <a name="to-set-source-control-options"></a>Per impostare le opzioni di controllo del codice sorgente  
  
1.  Scegliere **Opzioni** dal menu **Strumenti**.  
  
2.  Nel **opzioni** finestra di dialogo, espandere **controllo del codice sorgente**, quindi fare clic sul **Selezione plug-in** pagina.  
  
     **Plug-in del controllo del codice sorgente corrente**  
     Selezionare il controllo del codice sorgente desiderato nell'elenco. Il client del prodotto di controllo del codice sorgente deve essere installato sul computer, altrimenti non verrà visualizzato nell'elenco. Se sul computer non è installato alcun client di controllo del codice sorgente, l'unica selezione disponibile sarà Nessuno. Se è stata installato Microsoft Source Safe, vengono visualizzati i plug-in seguenti:  
  
    -   Microsoft Visual SourceSafe  
  
    -   Microsoft Visual SourceSafe (Internet)  
  
3.  Impostare le credenziali di accesso per ogni ruolo del controllo del codice sorgente che si desidera utilizzare. Questa pagina è disponibile solo se è installato un plug-in del controllo del codice sorgente.  
  
     **Descrizione del ruolo**  
     Le opzioni di controllo del codice sorgente vengono selezionate automaticamente in base al ruolo selezionato.  
  
    |Role|Descrizione|  
    |----------|-----------------|  
    |**Visual SourceSafe**|Specifica che si desidera usare le impostazioni usate più di frequente da [!INCLUDE[msCoName](../includes/msconame-md.md)] agli utenti di Visual SourceSafe.|  
    |**Sviluppatore indipendente**|Specifica che l'utente opera in modo indipendente.|  
    |**Custom**|Specifica che le impostazioni di un ruolo sono state modificate.|  
  
     **Eseguire gli aggiornamenti di stato in background**  
     Consente di aggiornare automaticamente le icone di segnalazione del controllo del codice sorgente in Esplora soluzioni nel momento in cui lo stato di un elemento cambia. Se si verificano ritardi durante l'esecuzione di operazioni particolarmente impegnative per il server, soprattutto durante l'apertura di una soluzione o un progetto dal controllo del codice sorgente, la deselezione di questa casella di controllo potrebbe migliorare le prestazioni.  
  
     **ID accesso**  
     Consente di specificare il nome utente da utilizzare per l'accesso al provider del controllo del codice sorgente. Se supportato dal provider del controllo, questo nome verrà immesso automaticamente nel **account di accesso** finestra di dialogo per raggiungere il server di controllo di origine. Per rendere attiva questa opzione, disabilitare gli accessi utente automatici utilizzando il programma di amministrazione del provider del controllo del codice sorgente e quindi riavviare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
     **Advanced**  
     Consente di visualizzare le opzioni aggiuntive per l'aggiunta di elementi al controllo del codice sorgente. Queste opzioni variano a seconda del provider del controllo del codice sorgente utilizzato. Per ulteriori informazioni su questi opzioni, fare riferimento al programma del controllo del codice sorgente.  
  
4.  Selezionare il **ambiente** pagina.  
  
5.  Nel **impostazioni di ambiente controllo sorgente** , selezionare il ruolo in cui si desidera impostare le opzioni di controllo di origine.  
  
     [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] seleziona automaticamente le opzioni di controllo del codice sorgente predefinite per il ruolo selezionato. Se si deselezionano opzioni predefinite, il **impostazioni di ambiente controllo di origine** verranno visualizzati nella **Custom** opzione per indicare che è stato personalizzato il ruolo selezionato originale.  
  
     **Impostazioni di ambiente controllo di origine**  
     Specifica il ruolo che si desidera utilizzare. In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] sono definiti i ruoli seguenti.  
  
    |Role|Descrizione|  
    |----------|-----------------|  
    |**Visual SourceSafe**|Specifica che si desidera usare le impostazioni usate più di frequente da [!INCLUDE[msCoName](../includes/msconame-md.md)] agli utenti di Visual SourceSafe.|  
    |**Sviluppatore indipendente**|Specifica che l'utente opera in modo indipendente.|  
    |**Custom**|Specifica che le impostazioni di un ruolo sono state modificate.|  
  
     Le opzioni di controllo del codice sorgente vengono selezionate automaticamente in base al ruolo selezionato.  
  
     **Mantieni gli elementi estratti durante l'archiviazione**  
     Consente di specificare che si desidera lasciare estratti gli elementi durante l'archiviazione per aggiornare l'archivio del controllo del codice sorgente. Se si desidera modificare questa opzione per un controllo specifico, fare clic sul **opzioni** freccia nel **Archivia** nella finestra di dialogo e quindi deselezionare la **Mantieni estratte** casella di controllo.  
  
     **Elementi archiviati**  
     Visualizza un elenco di opzioni che specificano come [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] comportamento quando si tenta di modificare un elemento non estratto. Le tabelle seguenti descrivono le opzioni disponibili.  
  
     **Il salvataggio**  
  
    |Azione|Descrizione|  
    |------------|-----------------|  
    |**Richiedi estrazione**|Consente di visualizzare il **Estrai** nella finestra di dialogo.|  
    |**Estrai automaticamente**|Estrae gli elementi senza visualizzare la **Estrai** nella finestra di dialogo. Si tratta dell'opzione predefinita.|  
    |**Salva con nome**|Salva come nuovo file.|  
  
     **La modifica**  
  
    |Azione|Descrizione|  
    |------------|-----------------|  
    |**Richiedi estrazione**|Consente di visualizzare il **Estrai** nella finestra di dialogo.|  
    |**Richiedi estrazioni in modo esclusivi**|Consente di visualizzare il **Estrai** nella finestra di dialogo.|  
    |**Estrai automaticamente**|Estrae gli elementi senza visualizzare la **Estrai** nella finestra di dialogo. Si tratta dell'opzione predefinita.|  
    |**Non eseguire alcuna operazione**|Non esegue l'estrazione del file.|  
  
     **Consenti gli elementi archiviati da modificare**  
     Specifica che gli elementi archiviati possono essere modificati nella memoria. Se si seleziona questa casella di controllo, un **modifica** pulsante viene visualizzato nel **Check Out** quando si tenta di modificare un elemento archiviato nella finestra di dialogo. Dopo avere fatto clic su questo pulsante è possibile modificare l'elemento. Se si desidera salvare l'elemento, è necessario estrarlo o salvarlo in un percorso diverso.  
  
     **Reimposta**  
     Reimposta le impostazioni predefinite delle finestre di dialogo di conferma del controllo del codice sorgente. Ad esempio, se è stata selezionata la **non visualizzare più questa finestra di dialogo** casella di controllo in una finestra di dialogo controllo codice sorgente, selezionando il **reimpostare** opzione Annulla tale azione.  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali di controlli di origine](../../2014/database-engine/source-control-basics.md)   
 [Modificare le connessioni di controllo di origine](../../2014/database-engine/change-source-control-connections.md)   
 [Esclusione di file dal controllo del codice sorgente](../../2014/database-engine/exclude-files-from-source-control.md)  
  
  
