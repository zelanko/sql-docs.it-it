---
title: Progetti (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c13af859-ca66-4e43-b76a-0650ac6566c0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 85bc34af971db386862528ac36ea04fef33f2daa
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52759193"
---
# <a name="projects-sql-server-management-studio"></a>Progetti (SQL Server Management Studio)
  Un progetto di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] è una raccolta di file e script correlati logicamente che possono essere salvati insieme per l'amministrazione e lo sviluppo del database.  
  
## <a name="script-project-overview"></a>Panoramica sui progetti script  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] I progetti script vengono visualizzati nel componente Esplora soluzioni di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Un progetto script può contenere zero o più file di progetto. È possibile aggiungere un progetto a una soluzione oppure combinare più progetti all'interno di una soluzione.  
  
 I progetti possono includere quanto segue:  
  
-   **Connessioni**. Una connessione, come si presenta all'interno di un progetto, contiene le informazioni relative all'account di accesso, il nome del server, il database predefinito, il protocollo adottato, il tipo di autenticazione e le proprietà di connessione. Se lo si desidera è possibile archiviare le informazioni di connessione con uno script (vedere di seguito).  
  
-   **Script SQL**. Script SQL utilizzati frequentemente dall'utente. Facendo doppio clic su un file con estensione sql all'interno del progetto, lo script selezionato verrà aperto nell'editor SQL.  
  
-   **Script MDX, DMX e XMLA**. Script MDX utilizzati frequentemente dall'utente. Facendo doppio clic su un file con estensione mdx all'interno del progetto, lo script selezionato verrà aperto nell'editor.  
  
-   **Varie**. È possibile utilizzare questa cartella per i file che non rientrano esattamente in nessuno degli altri tipi di nodo predefiniti, ad esempio un file di testo che contiene gli obiettivi del progetto.  
  
 I progetti possono inoltre essere integrati in un sistema di controllo del codice sorgente.  
  
## <a name="connecting-to-an-instance-of-sql-server-from-a-script-project"></a>Connessione a un'istanza di SQL Server da un progetto script  
 Un progetto script può contenere connessioni a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un progetto facendo clic sulla connessione. Verrà visualizzata una finestra Script SQL connessa all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definita nella connessione selezionata. Se si apre uno script di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o MDX con una connessione che usa l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , verrà richiesto di immettere la password usando la finestra di dialogo **Connetti a SQL Server** dopo l'apertura dell'editor e il caricamento dello script.  
  
 La connessione verrà chiusa dopo la chiusura della finestra corrispondente.  
  
 Per modificare le informazioni su una connessione, utilizzare la finestra delle proprietà in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## <a name="project-tasks"></a>Attività di progetto  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Viene descritto come creare un nuovo progetto in una soluzione.|[Creare un progetto](create-a-project.md)|  
|Viene descritto come aggiungere un progetto esistente a una soluzione.|[Aggiunta di un progetto esistente a una soluzione](add-an-existing-project-to-a-solution.md)|  
|Viene descritto come modificare il percorso predefinito in cui vengono salvati i file di progetto.|[Modifica del percorso predefinito per i progetti](change-the-default-location-for-projects.md)|  
|Viene descritto come visualizzare le proprietà correnti di un progetto.|[Visualizzare le proprietà di un progetto](view-project-properties.md)|  
|Viene descritto come aggiungere nuovi elementi, ad esempio connessioni o file di script, a un progetto.|[Aggiungere nuovi elementi a un progetto](add-new-items-to-a-project.md)|  
|Viene descritto come definire le informazioni di connessione per una query.|[Associazione di una query a una connessione in un progetto](associate-a-query-with-a-connection-in-a-project.md)|  
|Viene descritto come modificare le informazioni di connessione per una query.|[Modificare la connessione associata a una query](change-the-connection-associated-with-a-query.md)|  
|Viene descritto come modificare le proprietà di connessione.|[Visualizzazione o modifica delle proprietà di una connessione in un progetto](view-or-change-the-properties-of-a-connection-in-a-project.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esplora soluzioni](solution-explorer.md)   
 [Soluzioni di &#40;SQL Server Management Studio&#41;](solutions-sql-server-management-studio.md)   
 [Controllo del codice sorgente di Esplora soluzioni](../../database-engine/solution-explorer-source-control.md)  
  
  
