---
title: Gestione connessione OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- OLE DB connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], OLE DB
- connections [Integration Services], OLE DB
ms.assetid: 91e3622e-4b1a-439a-80c7-a00b90d66979
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 601e3b906a8c10d6f073eb05b3f62857f8c79bac
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58390467"
---
# <a name="ole-db-connection-manager"></a>gestione connessione OLE DB
  Una gestione connessione OLE DB consente la connessione di un pacchetto a un'origine dati tramite un provider OLE DB. In una gestione connessione OLE DB tramite che si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ad esempio, è possibile usare il provider [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]
>  Il provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 non supporta le nuove parole chiave per le stringhe di connessione (MultiSubnetFailover=True) per il clustering di failover su più subnet. Per altre informazioni, vedere la [note sulla versione di SQL Server](https://go.microsoft.com/fwlink/?LinkId=247824) e il post di blog [Failover su più Subnet AlwaysOn e SSIS](https://go.microsoft.com/fwlink/?LinkId=247825), su www.mattmasson.com.  
  
 La gestione connessione OLE DB viene usata da diversi componenti di flusso di dati e attività di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . L'origine e la destinazione OLE DB, ad esempio, usano questa gestione connessione per estrarre e caricare i dati, mentre l'attività Esegui SQL può usarla per connettersi a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'esecuzione delle query.  
  
 La gestione connessione OLE DB viene inoltre utilizzata per accedere alle origini dei dati OLE DB nelle attività personalizzate scritte in codice non gestito che utilizza un linguaggio quale C++.  
  
 Quando si aggiunge una gestione connessione OLE DB a un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione OLE DB, imposta le proprietà di tale gestione connessione e quindi la aggiunge alla raccolta `Connections` del pacchetto.  
  
 La proprietà `ConnectionManagerType` della gestione connessione viene impostata su `OLEDB`.  
  
 Per configurare la gestione connessione OLE DB, procedere nel modo seguente:  
  
-   Specificare una stringa di connessione configurata in modo da soddisfare i requisiti del provider selezionato.  
  
-   Se richiesto dal provider, includere il nome dell'origine dei dati a cui connettersi.  
  
-   Specificare le credenziali di sicurezza come previsto dal provider selezionato.  
  
-   Indicare se la connessione creata dalla gestione connessione deve essere mantenuta in fase di esecuzione.  
  
## <a name="logging"></a>Registrazione  
 È possibile registrare le chiamate eseguite dalla gestione connessione OLE DB a provider di dati esterni. Questa nuova funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi alle connessioni stabilite dalla gestione connessione OLE DB a origini dati esterne. Per registrare le chiamate eseguite dalla gestione connessione OLE DB a provider di dati esterni, abilitare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** a livello di pacchetto. Per altre informazioni, vedere [Strumenti per la risoluzione dei problemi relativi all'esecuzione dei pacchetti](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuration-of-the-oledb-connection-manager"></a>Configurazione della gestione connessione OLEDB  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice. Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Configura gestione connessione OLE DB](../configure-ole-db-connection-manager.md). Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere la documentazione per la classe **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** nella Guida per gli sviluppatori.  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Articolo di Wiki [SSIS with Oracle Connectors](https://go.microsoft.com/fwlink/?LinkId=220670) (Connettori SSIS con Oracle) nel sito Web social.technet.microsoft.com.  
  
-   Articolo tecnico [Connection Strings for OLE DB Providers](https://go.microsoft.com/fwlink/?LinkId=220744)(Stringhe di connessione per i provider OLE DB) nel sito Web carlprothman.net.  
  
## <a name="see-also"></a>Vedere anche  
 [Origine OLE DB](../data-flow/ole-db-source.md)   
 [Destinazione OLE DB](../data-flow/ole-db-destination.md)   
 [Attività Esegui SQL](../control-flow/execute-sql-task.md)   
 [Connessioni in Integration Services &#40;SSIS&#41;](integration-services-ssis-connections.md)  
  
  
