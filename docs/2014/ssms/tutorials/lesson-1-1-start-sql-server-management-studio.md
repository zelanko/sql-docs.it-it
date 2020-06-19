---
title: Avviare SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 25ffaea6-0eee-4169-8dd0-1da417c28fc6
author: stevestein
ms.author: sstein
ms.openlocfilehash: b8c74a4c427e4fc89d32c0dcf961bf5f4b839fff
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061965"
---
# <a name="start-sql-server-management-studio"></a>Avviare SQL Server Management Studio
  Prima di iniziare questa esercitazione è opportuno esaminare brevemente [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="opening-sql-server-management-studio"></a>Apertura di SQL Server Management Studio  
  
#### <a name="to-open-sql-server-management-studio"></a>Per aprire SQL Server Management Studio  
  
1.  Dal menu **Start** scegliere **tutti i programmi**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] e quindi fare clic su **SQL Server Management Studio**.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] non è installato per impostazione predefinita. Se [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] non è disponibile, installarlo eseguendo il programma di installazione. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] non è disponibile con [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]Express è disponibile come download gratuito dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=14630), ma dispone di un'interfaccia utente diversa da quella descritta in questa esercitazione.  
  
2.  Nella finestra di dialogo **Connetti al server** verificare le impostazioni predefinite e quindi fare clic su **Connetti**. Per connettersi, nella casella **nome server** deve essere contenuto il nome del computer in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è installato. Se [!INCLUDE[ssDE](../../includes/ssde-md.md)] è un'istanza denominata, nella casella **nome server** deve essere contenuto anche il nome dell'istanza nel formato \<*computer_name*> \\ < *instance_name*>.  
  
## <a name="management-studio-components"></a>Componenti di Management Studio  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] offre informazioni in finestre dedicate a tipi di informazioni specifiche. Le informazioni di database vengono visualizzate in Esplora oggetti e nelle finestre dei documenti.  
  
-   In Esplora oggetti è visualizzato l'albero di tutti gli oggetti di database presenti in un server. Possono essere inclusi i database del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Esplora oggetti contiene informazioni su tutti i server ai quali è connesso. All'apertura di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]viene chiesto di connettere Esplora oggetti alle ultime impostazioni utilizzate. È possibile fare doppio clic su un qualsiasi server nel componente Server registrati per eseguire la connessione, tuttavia non è necessario registrare un server per connettersi.  
  
-   La finestra del documento rappresenta la parte più estesa di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Le finestre dei documenti possono contenere editor di query e finestre del browser. Per impostazione predefinita, viene visualizzata la pagina Riepilogo connessa all'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] nel computer corrente.  
  
## <a name="showing-additional-windows"></a>Visualizzazione di finestre aggiuntive  
  
#### <a name="to-show-the-registered-servers-window"></a>Per visualizzare la finestra Server registrati  
  
1.  Scegliere **Server registrati** dal menu **Visualizza**.  
  
     La finestra Server registrati verrà visualizzata sopra Esplora oggetti. In Server registrati sono elencati i server gestiti più di frequente. È possibile aggiungere e rimuovere server dall'elenco. Gli unici server elencati saranno le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel computer in cui si esegue [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Se il server non viene visualizzato, in Server registrati fare clic con il pulsante destro del mouse su **motore di database**, quindi scegliere **Aggiorna registrazione server locale**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Connettersi con Server registrati ed Esplora oggetti](../object/object-explorer.md)  
  
  
