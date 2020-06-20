---
title: Nozioni fondamentali sul controllo del codice sorgente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- source controls [SQL Server Management Studio], providers
- source controls [SQL Server Management Studio]
- source controls [SQL Server Management Studio], about source controls
- source controls [SQL Server Management Studio], clients
ms.assetid: ca35b67a-104a-41fb-ac58-a61be06fe114
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: d28202148d6f85e0aafde6ee324b11fd8cd10b23
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84928934"
---
# <a name="source-control-basics"></a>Nozioni fondamentali sul controllo del codice sorgente
  Il controllo del codice sorgente è un sistema nel quale un componente centrale di un prodotto server archivia e tiene traccia delle versioni dei file, controllando inoltre l'accesso ai file. Un tipico sistema di controllo del codice sorgente include un provider di controllo del codice sorgente e due o più client di controllo del codice sorgente.  
  
## <a name="source-control-benefits"></a>Vantaggi del controllo del codice sorgente  
 L'inserimento dei file nel controllo del codice sorgente consente di:  
  
-   Gestire il processo tramite il quale il controllo degli elementi passa da una persona all'altra. I provider del controllo del codice sorgente supportano l'accesso ai file sia condiviso sia esclusivo. Se si accede ai file di progetto in modalità esclusiva, il provider consente a un solo utente alla volta di estrarre e modificare i file. Se l'accesso è condiviso, più utenti possono estrarre il file di script e il provider offre un meccanismo per eseguire l'unione delle versioni man mano che vengono archiviate.  
  
-   Archiviare versioni successive degli elementi inclusi nel controllo del codice sorgente. Un provider del controllo del codice sorgente archivia i dati che distinguono le varie versioni di un elemento incluso nel controllo del codice sorgente. Il provider archivia le differenze tra le versioni, oltre a informazioni essenziali sulla versione, quali la data di creazione e di modifica e l'autore. Se più persone lavorano allo stesso file, queste devono utilizzare la stessa tabella codici, in modo da poter confrontare con precisione le diverse versioni. È pertanto possibile recuperare qualsiasi versione di un elemento incluso nel controllo del codice sorgente e specificare inoltre quale deve essere l'ultima versione dell'elemento.  
  
-   Mantenere informazioni dettagliate sulla versione e sulla cronologia relative agli elementi inclusi nel controllo del codice sorgente. Nel controllo del codice sorgente vengono archiviate la data e l'ora di creazione dell'elemento, della sua estrazione o archiviazione e il nome dell'utente che ha eseguito l'azione.  
  
-   Collaborare a più progetti. La condivisione dei file consente la condivisione tra più progetti degli elementi inclusi nel controllo del codice sorgente. Le modifiche apportate a un elemento condiviso verranno applicate a tutti i progetti che condividono quell'elemento.  
  
-   Automatizzare le operazioni del controllo del codice sorgente ripetute di frequente. Un provider del controllo del codice sorgente può definire un'interfaccia dal prompt dei comandi che supporta le funzionalità principali del controllo del codice sorgente. È possibile utilizzare questa interfaccia nei file batch per automatizzare le attività di controllo del codice sorgente eseguite regolarmente.  
  
-   Eseguire il recupero dopo eliminazioni accidentali. È possibile ripristinare l'ultima versione del file archiviata nel controllo del codice sorgente.  
  
-   Risparmiare spazio su disco sia nel client sia nel server del controllo del codice sorgente. Alcuni provider del controllo del codice sorgente, ad esempio [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe, supportano la funzionalità di risparmio dello spazio su disco nel server archiviando l'ultima versione di un file e le differenze tra ogni versione e la versione precedente o successiva. Nel client Visual SourceSafe supporta il risparmio dello spazio su disco. È possibile mascherare cartelle e file per impedire che vengano scaricati nel disco locale.  
  
 Le estrazioni e le archiviazioni dei file, nonché altre operazioni di controllo del codice sorgente, vengono eseguite tramite un client di controllo del codice sorgente, ad esempio [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Il client è progettato per interagire con il provider in modo da rendere le funzionalità del provider disponibili per un gruppo di utenti distribuito. Un client di controllo del codice sorgente consente di esplorare i file archiviati dal provider, aggiungere ed eliminare file, eseguirne l'estrazione o l'archiviazione e recuperare copie di file locali.  
  
> [!NOTE]  
>  In questa documentazione si presuppone l'utilizzo di [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe come provider del controllo del codice sorgente. Se si utilizza un provider diverso, potrebbero esservi delle differenze tra questa documentazione e il software in uso. In questo caso, consultare la documentazione del provider del controllo del codice sorgente utilizzato.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|||  
|-|-|  
|**Attività**|**Argomento**|  
|Impostare le opzioni di controllo del codice sorgente|[Impostare le opzioni di controllo del codice sorgente](../../2014/database-engine/set-source-control-options.md)|  
|Modificare le connessioni del controllo del codice sorgente|[Modifica delle connessioni del controllo del codice sorgente](../../2014/database-engine/change-source-control-connections.md)|  
|Escludere file dal controllo del codice sorgente|[Esclusione di file dal controllo del codice sorgente](../../2014/database-engine/exclude-files-from-source-control.md)|  
  
  
