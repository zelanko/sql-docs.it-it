---
title: Impostare le opzioni di controllo del codice sorgente | Microsoft Docs
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
ms.openlocfilehash: 5ab6d134177c7861c3a8f92cf767c71c0b56e233
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929142"
---
# <a name="set-source-control-options"></a>Impostare le opzioni di controllo del codice sorgente
  Per utilizzare le caratteristiche di controllo del codice sorgente incorporate in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], è necessario configurare le relative opzioni per i diversi ambienti di lavoro.  
  
 Per configurare le opzioni di controllo del codice sorgente, utilizzare la finestra di dialogo **Opzioni** per configurare uno o più ruoli del controllo del codice sorgente. Un ruolo è una descrizione generale dell'impostazione utilizzata per [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e delle opzioni di controllo del codice sorgente associate a questa impostazione.  
  
 Ad esempio, uno sviluppatore di database indipendente generalmente non crea conflitti con altri utenti mantenendo file estratti dopo averli archiviati. Di conseguenza, in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] viene definito un ruolo Sviluppatore Indipendente. Per questo ruolo, [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] Seleziona automaticamente l'opzione **Mantieni gli elementi estratti durante l'archiviazione** .  
  
 Poiché i ruoli possono essere definiti e personalizzati, è possibile lavorare con impostazioni di sviluppo diverse senza riconfigurare completamente il controllo del codice sorgente ogni volta che si passa da un'impostazione all'altra.  
  
### <a name="to-set-source-control-options"></a>Per impostare le opzioni di controllo del codice sorgente  
  
1.  Scegliere **Opzioni** dal menu **Strumenti**.  
  
2.  Nella finestra di dialogo **Opzioni** espandere **controllo del codice sorgente**, quindi fare clic sulla pagina **Selezione plug-in** .  
  
     **Plug-in del controllo del codice sorgente corrente**  
     Selezionare il controllo del codice sorgente desiderato nell'elenco. Il client del prodotto di controllo del codice sorgente deve essere installato sul computer, altrimenti non verrà visualizzato nell'elenco. Se sul computer non è installato alcun client di controllo del codice sorgente, l'unica selezione disponibile sarà Nessuno. Se è stata installato Microsoft Source Safe, vengono visualizzati i plug-in seguenti:  
  
    -   Microsoft Visual SourceSafe  
  
    -   Microsoft Visual SourceSafe (Internet)  
  
3.  Impostare le credenziali di accesso per ogni ruolo del controllo del codice sorgente che si desidera utilizzare. Questa pagina è disponibile solo se è installato un plug-in del controllo del codice sorgente.  
  
     **Role Description**  
     Le opzioni di controllo del codice sorgente vengono selezionate automaticamente in base al ruolo selezionato.  
  
    |Ruolo|Descrizione|  
    |----------|-----------------|  
    |**Visual SourceSafe**|Specifica che si desidera utilizzare le impostazioni utilizzate più di frequente dagli [!INCLUDE[msCoName](../includes/msconame-md.md)] utenti di Visual SourceSafe.|  
    |**Sviluppatore indipendente**|Specifica che l'utente opera in modo indipendente.|  
    |**Impostazione personalizzata**|Specifica che le impostazioni di un ruolo sono state modificate.|  
  
     **Esegui gli aggiornamenti dello stato in background**  
     Consente di aggiornare automaticamente le icone di segnalazione del controllo del codice sorgente in Esplora soluzioni nel momento in cui lo stato di un elemento cambia. Se si verificano ritardi durante l'esecuzione di operazioni particolarmente impegnative per il server, soprattutto durante l'apertura di una soluzione o un progetto dal controllo del codice sorgente, la deselezione di questa casella di controllo potrebbe migliorare le prestazioni.  
  
     **ID di accesso**  
     Consente di specificare il nome utente da utilizzare per l'accesso al provider del controllo del codice sorgente. Se supportato dal provider del controllo del codice sorgente, questo nome verrà compilato automaticamente nella finestra di dialogo di **accesso** per raggiungere il server del controllo del codice sorgente. Per rendere attiva questa opzione, disabilitare gli accessi utente automatici utilizzando il programma di amministrazione del provider del controllo del codice sorgente e quindi riavviare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
     **Avanzate**  
     Consente di visualizzare le opzioni aggiuntive per l'aggiunta di elementi al controllo del codice sorgente. Queste opzioni variano a seconda del provider del controllo del codice sorgente utilizzato. Per ulteriori informazioni su questi opzioni, fare riferimento al programma del controllo del codice sorgente.  
  
4.  Selezionare la pagina **ambiente** .  
  
5.  Nella casella **impostazioni di ambiente controllo del codice sorgente** selezionare il ruolo per il quale si desidera impostare le opzioni di controllo del codice sorgente.  
  
     [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] seleziona automaticamente le opzioni di controllo del codice sorgente predefinite per il ruolo selezionato. Se si deseleziona una delle opzioni predefinite, nella casella **impostazioni di ambiente controllo del codice sorgente** viene visualizzata l'opzione **personalizzata** per indicare che è stato personalizzato il ruolo selezionato originariamente.  
  
     **Impostazioni di ambiente controllo del codice sorgente**  
     Specifica il ruolo che si desidera utilizzare. In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] sono definiti i ruoli seguenti.  
  
    |Ruolo|Descrizione|  
    |----------|-----------------|  
    |**Visual SourceSafe**|Specifica che si desidera utilizzare le impostazioni utilizzate più di frequente dagli [!INCLUDE[msCoName](../includes/msconame-md.md)] utenti di Visual SourceSafe.|  
    |**Sviluppatore indipendente**|Specifica che l'utente opera in modo indipendente.|  
    |**Impostazione personalizzata**|Specifica che le impostazioni di un ruolo sono state modificate.|  
  
     Le opzioni di controllo del codice sorgente vengono selezionate automaticamente in base al ruolo selezionato.  
  
     **Mantieni gli elementi estratti durante l'archiviazione**  
     Consente di specificare che si desidera lasciare estratti gli elementi durante l'archiviazione per aggiornare l'archivio del controllo del codice sorgente. Se si desidera modificare questa opzione per un'archiviazione specifica, fare clic sulla freccia **Opzioni** nella finestra di dialogo **Archivia** , quindi deselezionare la casella di controllo **Mantieni estratto** .  
  
     **Comportamento degli elementi archiviati**  
     Visualizza un elenco di opzioni che specificano come [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] si comporterà quando si tenta di modificare un elemento non estratto. Le tabelle seguenti descrivono le opzioni disponibili.  
  
     **Risparmio**  
  
    |Azione|Descrizione|  
    |------------|-----------------|  
    |**Richiedi estrazione**|Consente di visualizzare la finestra di dialogo **Estrai** .|  
    |**Estrai automaticamente**|Estrae l'elemento senza visualizzare la finestra di dialogo **Estrai** . Questa è l'opzione predefinita.|  
    |**Salva con nome**|Salva come nuovo file.|  
  
     **In fase di modifica**  
  
    |Azione|Descrizione|  
    |------------|-----------------|  
    |**Richiedi estrazione**|Consente di visualizzare la finestra di dialogo **Estrai** .|  
    |**Richiedi estrazioni in modo esclusivo**|Consente di visualizzare la finestra di dialogo **Estrai** .|  
    |**Estrai automaticamente**|Estrae l'elemento senza visualizzare la finestra di dialogo **Estrai** . Questa è l'opzione predefinita.|  
    |**Non eseguire alcuna operazione**|Non esegue l'estrazione del file.|  
  
     **Consenti modifica degli elementi archiviati**  
     Specifica che gli elementi archiviati possono essere modificati nella memoria. Se si seleziona questa casella di controllo, viene visualizzato un pulsante **modifica** nella finestra di dialogo **Estrai** quando si tenta di modificare un elemento archiviato. Dopo avere fatto clic su questo pulsante è possibile modificare l'elemento. Se si desidera salvare l'elemento, è necessario estrarlo o salvarlo in un percorso diverso.  
  
     **Reimposta**  
     Reimposta le impostazioni predefinite delle finestre di dialogo di conferma del controllo del codice sorgente. Ad esempio, se è stata selezionata la casella di controllo **non visualizzare più questa finestra** di dialogo in una finestra di dialogo del controllo del codice sorgente, se si seleziona l'opzione **Reimposta** l'azione verrà annullata.  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali sul controllo del codice sorgente](../../2014/database-engine/source-control-basics.md)   
 [Modificare le connessioni del controllo del codice sorgente](../../2014/database-engine/change-source-control-connections.md)   
 [Esclusione di file dal controllo del codice sorgente](../../2014/database-engine/exclude-files-from-source-control.md)  
  
  
