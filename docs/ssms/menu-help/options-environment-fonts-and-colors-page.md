---
description: Opzioni (Ambiente- pagina Tipi di carattere e colori)
title: Opzioni (Ambiente- pagina Tipi di carattere e colori)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: ea3aa222-538d-485f-99dc-01eb02cdcfea
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8981ada42e88eadcb263e01dd65f1b2cf9015852
ms.sourcegitcommit: 827ad02375793090fa8fee63cc372d130f11393f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2020
ms.locfileid: "89480233"
---
# <a name="options-environment---fonts-and-colors-page"></a>Opzioni (Ambiente- pagina Tipi di carattere e colori)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
La finestra di dialogo **Opzioni** consente di specificare una combinazione colori e un tipo di carattere personalizzati per vari elementi dell'interfaccia utente in [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Scegliere **Opzioni** dal menu **Strumenti** , espandere la cartella **Ambiente** e selezionare **Tipi di carattere e colori**.  
  
Le modifiche apportate alla combinazione colori non diventano effettive durante la sessione in cui vengono eseguite. Per valutare le modifiche dei colori, aprire un'altra istanza di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e riprodurre le condizioni in cui si prevede che tali modifiche vengano applicate.  
  
## <a name="ui-element-list"></a>Elenco di elementi dell'interfaccia utente  
**Mostra impostazioni per**  
Consente di visualizzare l'elenco di tutti gli elementi dell'interfaccia utente per i quali è possibile modificare le combinazioni colori e i tipi di carattere. Dopo aver selezionato un elemento da questo elenco, è possibile personalizzare le impostazioni dei colori per l'elemento selezionato in **Elementi visualizzati**.  
  
|Termine|Definizione|  
|--------|--------------|  
|Editor di testo|Le modifiche delle impostazioni di visualizzazione dello stile, della dimensione e del colore del tipo di carattere dell'editor di testo influiscono sull'aspetto del testo nell'editor predefinito. I documenti aperti in un editor di testo all'esterno di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] non verranno influenzati da queste impostazioni.|  
|Stampante|Le modifiche delle impostazioni di visualizzazione dello stile, della dimensione e del colore della stampante influiscono sull'aspetto del testo nei documenti stampati.<br /><br />Nota: è possibile selezionare un tipo di carattere predefinito per la stampa diverso da quello usato per la visualizzazione nell'editor di testo. Questa operazione può essere utile quando si esegue la stampa di codice contenente sia caratteri SBCS sia caratteri DBCS.|  
|[Tutte le finestre degli strumenti di testo **]**|Le modifiche delle impostazioni di visualizzazione dello stile, della dimensione e del colore del tipo di carattere per questo elemento influiscono sull'aspetto del testo nelle finestre degli strumenti contenenti riquadri di output in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ad esempio la finestra di output, la finestra Risultati in formato testo e così via.<br /><br />Nota: le modifiche apportate al testo degli elementi di [Tutte le finestre degli strumenti di testo] non diventano effettive durante la sessione in cui vengono eseguite. Per valutare tali modifiche, aprire un'altra istanza di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
|Finestra Risultati ricerca|Le modifiche delle impostazioni di visualizzazione dello stile, della dimensione e del colore del tipo di carattere per questo elemento influiscono sull'aspetto del testo nella finestra Risultati ricerca.|  
|Finestra di output|Le modifiche delle impostazioni di visualizzazione dello stile, della dimensione e del colore del tipo di carattere per questo elemento influiscono sull'aspetto del testo nella finestra di output.|  
|Risultati in formato griglia|Le modifiche delle impostazioni di visualizzazione dello stile, della dimensione e del colore del tipo di carattere per questo elemento influiscono sull'aspetto del testo nell'area **Risultati in formato griglia** della finestra Query.|  
|Piano di esecuzione|Le modifiche delle impostazioni di visualizzazione dello stile, della dimensione e del colore del tipo di carattere per questo elemento influiscono sull'aspetto del testo in Piano di esecuzione delle query di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssEW](../../includes/ssew-md.md)].|  
|Risultati in formato testo|Le modifiche delle impostazioni di visualizzazione dello stile, della dimensione e del colore del tipo di carattere per questo elemento influiscono sull'aspetto del testo nell'area **Risultati in formato testo** della finestra Query.|  
|Finestre di progettazione Business Intelligence|Le modifiche delle impostazioni di visualizzazione dello stile, della dimensione e del colore del tipo di carattere per questo elemento influiscono sull'aspetto del testo nelle finestre di Progettazione di Business Intelligence .|  
  
**Valori predefiniti**  
Il pulsante **Valori predefiniti** reimposta i valori predefiniti del tipo di carattere e dei colori dell'elemento selezionato dall'elenco **Mostra impostazioni per** .  
  
**Carattere (tipi di carattere a larghezza fissa in grassetto)**  
Consente di visualizzare l'elenco di tutti i tipi di carattere installati nel sistema. Quando si apre questo elenco a discesa per la prima volta, viene selezionato il tipo di carattere corrente dell'elemento scelto nell'elenco **Mostra impostazioni per** . I tipi di carattere a larghezza fissa, più facili da allineare in un editor, vengono visualizzati in grassetto.  
  
**Dimensione**  
Consente di visualizzare le dimensioni in punti disponibili per il tipo di carattere selezionato. La modifica delle dimensioni del tipo di carattere influisce su tutte le voci di **Elementi visualizzati** relative a una selezione di **Mostra impostazioni per** .  
  
**Elementi visualizzati**  
Consente di visualizzare l'elenco di tutti gli elementi di cui è possibile modificare il colore di primo piano e quello di sfondo.  
  
> [!NOTE]  
> **L**'elemento di visualizzazione predefinito è Testo. Le proprietà assegnate a Testo verranno pertanto sovrascritte dalle proprietà assegnate ad altri elementi di visualizzazione. Se ad esempio si assegna il colore blu a **Testo** e il colore verde a Identificatore, tutti gli identificatori verranno visualizzati in verde. In questo esempio le proprietà di Identificatore sovrascrivono quelle di Testo.  
  
Alcuni elementi di visualizzazione includono:  
  
-   Margine indicatore, ovvero il margine a sinistra dell'editor del codice in cui vengono visualizzati i punti di interruzione e le icone dei segnalibri.  
  
-   Testo comprimibile, ovvero un blocco di testo o di codice che può essere visualizzato o meno all'interno dell'editor del codice (solo XML).  
  
**Primo piano elemento**  
Visualizza l'elenco dei colori disponibili che è possibile scegliere per il primo piano dell'elemento selezionato in **Elementi visualizzati**. Poiché alcuni elementi sono correlati, deve essere mantenuto uno schema di visualizzazione coerente. La modifica del colore di primo piano del testo, ad esempio, modifica anche il colore di primo piano di elementi come Stringa.  
  
**Impostazione personalizzata**  
Visualizza la finestra di dialogo **Colore** , in cui è possibile impostare un colore personalizzato per l'elemento selezionato nell'elenco **Elementi visualizzati** .  
  
> [!NOTE]  
> La possibilità di definire colori personalizzati può venire limitata dalle impostazioni dei colori dello schermo del computer. Se, ad esempio, il computer è impostato sulla visualizzazione di 256 colori e si seleziona un colore personalizzato nella finestra di dialogo **Colore** , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] imposta come predefinito il colore più simile tra quelli disponibili in **Colori di base** e nella finestra di dialogo **Colore** viene visualizzato il colore nero.  
  
**Sfondo elemento**  
Visualizza una tavolozza di colori in cui è possibile scegliere un colore di sfondo per l'elemento selezionato in **Elementi visualizzati**. Poiché alcuni elementi sono correlati, deve essere mantenuto uno schema di visualizzazione coerente. La modifica del colore di sfondo del testo, ad esempio, modifica anche il colore di sfondo degli elementi come Stringa SQL.  
  
**Impostazione personalizzata**  
Visualizza la finestra di dialogo **Colore** , in cui è possibile impostare un colore personalizzato per l'elemento selezionato nell'elenco **Elementi visualizzati** .  
  
**Grassetto**  
Selezionare questa casella di controllo per visualizzare il testo degli elementi di visualizzazione selezionati in grassetto. Il testo in grassetto è più facile da identificare in un editor.  
  
**Esempio**  
Visualizza un esempio della combinazione colori, dello stile e della dimensione del tipo carattere relativi ai valori selezionati in **Mostra impostazioni per** ed **Elementi visualizzati**. È possibile utilizzare questa casella di testo per visualizzare un'anteprima dei risultati, mentre si provano diverse opzioni di formattazione.  
  
## <a name="see-also"></a>Vedere anche  
[Codifica tramite colori negli editor del codice](../../relational-databases/scripting/color-coding-in-query-editors.md)  