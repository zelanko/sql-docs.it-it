---
title: Controllo del codice sorgente Esplora soluzioni | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Visual SourceSafe
- SQL Server Management Studio [SQL Server], source control services
- source-controlled files [SQL Server]
- source controls [SQL Server Management Studio], services
- version control services [SQL Server]
- file source control services [SQL Server]
- VSS [Visual SourceSafe]
ms.assetid: 6373adb8-3d81-4945-a9fc-1d0d5799d29a
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 44843764b7eed26bfd424ee61f2534aae42b9a73
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84928982"
---
# <a name="solution-explorer-source-control"></a>Controllo del codice sorgente di Esplora soluzioni
  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]Esplora soluzioni possono essere integrati in un sistema di controllo del codice sorgente distinto. Dopo aver integrato una soluzione o un progetto in un sistema di controllo del codice sorgente, è possibile controllare l'accesso ai file e il controllo delle versioni per gli script e le query dei progetti.  
  
## <a name="solution-and-project-source-control"></a>Controllo del codice sorgente di soluzioni e progetti  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)]  
  
 Il controllo del codice sorgente è un sistema nel quale un componente centrale di un prodotto server archivia e tiene traccia delle versioni dei file, controllando inoltre l'accesso ai file. Un tipico sistema di controllo del codice sorgente include un provider di controllo del codice sorgente e due o più client di controllo del codice sorgente. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] può essere integrato con un servizio di controllo del codice sorgente. Ciò significa che è possibile utilizzare lo strumento come client per il provider di controllo del codice sorgente. Senza uscire dall'ambiente, è possibile gestire facilmente sia i progetti individuali che quelli di team. Il provider del controllo del codice sorgente non è incluso in [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
#### <a name="to-select-a-source-control-provider"></a>Per selezionare un provider del controllo del codice sorgente  
  
1.  Installare la parte client del provider del controllo del codice sorgente.  
  
2.  In [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], scegliere **Opzioni** dal menu **Strumenti**.  
  
3.  Nella finestra di dialogo **Opzioni** espandere **controllo del codice sorgente**, quindi fare clic sulla pagina **Selezione plug-in** .  
  
4.  Nella casella **plug-in del controllo del codice sorgente corrente** selezionare il plug-in del controllo del codice sorgente.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Nozioni fondamentali sul controllo del codice sorgente](../../2014/database-engine/source-control-basics.md)|Viene definita la terminologia di base del controllo del codice sorgente e vengono spiegati i vantaggi per il progetto offerti dai servizi di controllo del codice sorgente.|  
|[Aggiungere soluzioni e progetti al controllo del codice sorgente](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)|Viene spiegato come utilizzare l'ambiente [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] per aggiungere soluzioni e progetti al controllo del codice sorgente.|  
|[Apertura di soluzioni e progetti dal controllo del codice sorgente](../../2014/database-engine/open-solutions-and-projects-from-source-control.md)|Viene spiegato come utilizzare l'ambiente [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] per aprire soluzioni e progetti inclusi nel controllo del codice sorgente.|  
|[Gestione delle estrazioni](../../2014/database-engine/manage-checkouts.md)|Viene spiegato come estrarre soluzioni e file dal controllo del codice sorgente.|  
|[Gestione delle archiviazioni](../../2014/database-engine/manage-checkins.md)|Viene spiegato come archiviare soluzioni e file nel controllo del codice sorgente.|  
|[Impostazione e recupero delle informazioni sulla versione](../../2014/database-engine/set-and-retrieve-version-information.md)|Viene spiegato come recuperare la cronologia di un progetto o di un elemento, una copia locale di un elemento o come confrontare due versioni di un elemento.|  
|||  
  
## <a name="see-also"></a>Vedere anche  
 [Esplora soluzioni](../ssms/solution/solution-explorer.md)   
 [Soluzioni &#40;SQL Server Management Studio&#41;](../ssms/sql-server-management-studio-ssms.md)   
 [Progetti &#40;SQL Server Management Studio&#41;](../ssms/solution/projects-sql-server-management-studio.md)   
 [File per la gestione di soluzioni e progetti](../ssms/solution/files-that-manage-solutions-and-projects.md)  
  
  
