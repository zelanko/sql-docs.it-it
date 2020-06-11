---
title: "Errore durante il tentativo di stabilire una connessione all'origine dati esterna. Impossibile aggiornare le connessioni seguenti: dati PowerPivot | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1b951da1-f62d-43d2-b40b-270a4a9ab92c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 242fefb2ca22d7b0129268a8a3ea8ed98e80bbe3
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547613"
---
# <a name="an-error-occurred-during-an-attempt-to-establish-a-connection-to-the-external-data-source-the-following-connections-failed-to-refresh-powerpivot-data"></a>Errore durante il tentativo di stabilire una connessione all'origine dati esterna. Impossibile aggiornare le connessioni seguenti: Dati di PowerPivot
  Questo errore si verifica se si esegue una query sui dati PowerPivot in un server in cui non è installato PowerPivot per SharePoint. Si verifica anche se viene arrestato il servizio SQL Server Analysis Services (PowerPivot) o se si tenta di visualizzare dati PowerPivot di una versione precedente.  
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Si applica a|PowerPivot per SharePoint|  
|Versione prodotto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Impossibile stabilire la connessione dati.|  
|Testo del messaggio|Errore durante il tentativo di stabilire una connessione all'origine dati esterna. Impossibile aggiornare le connessioni seguenti: Dati di PowerPivot|  
  
## <a name="explanation"></a>Spiegazione  
 Excel Services restituisce questo errore quando si esegue una query sui dati PowerPivot in una cartella di lavoro di Excel pubblicata in SharePoint e l'ambiente SharePoint non include un server PowerPivot per SharePoint o se il servizio SQL Server Analysis Services (PowerPivot) è stato arrestato.  
  
 L'errore si verifica quando si sezionano o filtrano dati PowerPivot quando il motore di query non è disponibile.  
  
## <a name="user-action"></a>Azione dell'utente  
 Installare PowerPivot per SharePoint o spostare la cartella di lavoro di PowerPivot in un ambiente SharePoint in cui sia installato PowerPivot per SharePoint. Per ulteriori informazioni, vedere [PowerPivot for SharePoint 2010 Installation](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md).  
  
 Se il software è installato, verificare che l'istanza di SQL Server Analysis Services (PowerPivot) sia in esecuzione. Selezionare **Gestisci servizi nel server** in Amministrazione centrale. Selezionare inoltre l'applicazione console Servizi in Strumenti di amministrazione.  
  
 Per le cartelle di lavoro di PowerPivot create nella versione SQL Server 2008 R2 di PowerPivot per Excel è necessario installare la versione SQL Server 2008 R2 del provider OLE DB per Analysis Services. Si verificherà questo errore se è stato installato il provider, ma non è stato registrato il file Microsoft.AnalysisServices.ChannelTransport.dll. Per altre informazioni sulla registrazione dei file, vedere [Installazione del provider OLE DB di Analysis Services nei server di SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Per la connessione dati viene utilizzata l'autenticazione di Windows e non è stato possibile delegare le credenziali utente. Impossibile aggiornare le connessioni seguenti: dati PowerPivot](the-data-connection-user-could-not-be-delegated.md)  
  
  
