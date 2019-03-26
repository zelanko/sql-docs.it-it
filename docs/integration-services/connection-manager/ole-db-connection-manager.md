---
title: Gestione connessione OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbconnection.f1
helpviewer_keywords:
- OLE DB connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], OLE DB
- connections [Integration Services], OLE DB
ms.assetid: 91e3622e-4b1a-439a-80c7-a00b90d66979
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 859f9736c8f67bfbc49fd82f36011b7ee243b3b4
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58275956"
---
# <a name="ole-db-connection-manager"></a>gestione connessione OLE DB
  Una gestione connessione OLE DB consente la connessione di un pacchetto a un'origine dati tramite un provider OLE DB. In una gestione connessione OLE DB tramite che si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ad esempio, è possibile usare il provider [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
    
> [!NOTE]
>  Il provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 non supporta le nuove parole chiave per le stringhe di connessione (MultiSubnetFailover=True) per il clustering di failover su più subnet. Per altre informazioni, vedere le [note sulla versione di SQL Server](https://go.microsoft.com/fwlink/?LinkId=247824) e il post di blog [Always On Multi-Subnet Failover and SSIS](https://www.mattmasson.com/2012/03/alwayson-multi-subnet-failover-and-ssis/)(Failover su più subnet Always On e SSIS) nel sito www.mattmasson.com.    
> 
> [!NOTE]
>  Se l'origine dati è [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, è richiesto un provider di dati diverso rispetto alle versioni precedenti di Excel o Access. Per altre informazioni, vedere [Connettersi a una cartella di lavoro di Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md) e [Connettersi a un database di Access](../../integration-services/connection-manager/connect-to-an-access-database.md).    
    
 La gestione connessione OLE DB viene usata da diversi componenti di flusso di dati e attività di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . L'origine e la destinazione OLE DB, ad esempio, usano questa gestione connessione per estrarre e caricare i dati, mentre l'attività Esegui SQL può usarla per connettersi a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'esecuzione delle query.    
    
 La gestione connessione OLE DB viene inoltre utilizzata per accedere alle origini dei dati OLE DB nelle attività personalizzate scritte in codice non gestito che utilizza un linguaggio quale C++.    
    
 Quando si aggiunge una gestione connessione OLE DB a un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione OLE DB, imposta le proprietà di tale gestione connessione e quindi la aggiunge alla raccolta **Connessioni** del pacchetto.    
    
 La proprietà **ConnectionManagerType** della gestione connessione viene impostata su **OLEDB**.    
    
 Per configurare la gestione connessione OLE DB, procedere nel modo seguente:    
    
-   Specificare una stringa di connessione configurata in modo da soddisfare i requisiti del provider selezionato.    
    
-   Se richiesto dal provider, includere il nome dell'origine dei dati a cui connettersi.    
    
-   Specificare le credenziali di sicurezza come previsto dal provider selezionato.    
    
-   Indicare se la connessione creata dalla gestione connessione deve essere mantenuta in fase di esecuzione.    
    
## <a name="logging"></a>Registrazione    
 È possibile registrare le chiamate eseguite dalla gestione connessione OLE DB a provider di dati esterni. Questa nuova funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi alle connessioni stabilite dalla gestione connessione OLE DB a origini dati esterne. Per registrare le chiamate eseguite dalla gestione connessione OLE DB a provider di dati esterni, abilitare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** a livello di pacchetto. Per altre informazioni, vedere [Strumenti per la risoluzione dei problemi relativi all'esecuzione dei pacchetti](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).    
    
## <a name="configuration-of-the-oledb-connection-manager"></a>Configurazione della gestione connessione OLEDB    
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice. Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Configura gestione connessione OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md). Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere la documentazione per la classe **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** nella Guida per gli sviluppatori.    
    
## <a name="related-content"></a>Contenuto correlato    
    
-   Articolo di Wiki [SSIS with Oracle Connectors](https://go.microsoft.com/fwlink/?LinkId=220670) (Connettori SSIS con Oracle) nel sito Web social.technet.microsoft.com.    
    
-   Articolo tecnico [Connection Strings for OLE DB Providers](https://go.microsoft.com/fwlink/?LinkId=220744)(Stringhe di connessione per i provider OLE DB) nel sito Web carlprothman.net.    
    
## <a name="configure-ole-db-connection-manager"></a>Configura gestione connessione OLE DB
  Usare la finestra di dialogo **Configura gestione connessione OLE DB** per aggiungere una nuova connessione o una copia di una connessione esistente a un'origine dati.  
  
> [!NOTE]  
>  Se l'origine dati è [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, è richiesta una gestione connessione diversa rispetto alle versioni precedenti di Excel. Per altre informazioni, vedere [Connessione a una cartella di lavoro di Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
>   
>  Se l'origine dati è [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, è richiesto un provider OLE DB diverso rispetto alle versioni precedenti di Access. Per altre informazioni, vedere [Connessione a un database di Access](../../integration-services/connection-manager/connect-to-an-access-database.md).  
  
 Per sapere di più sulla gestione connessione OLE DB, vedere [Gestione connessione OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Connessioni dati**  
 Consente di selezionare una connessione dati OLE DB esistente nell'elenco.  
  
 **Proprietà connessione dati**  
 Consente di visualizzare proprietà e valori per la connessione dati OLE DB selezionata.  
  
 **Nuova**  
 Consente di creare una connessione dati OLE DB tramite la finestra di dialogo **Gestione connessione** .  
  
 **Elimina**  
 Selezionare una connessione dati, quindi eliminarla usando il pulsante **Elimina** .  
  
## <a name="see-also"></a>Vedere anche    
 [Origine OLE DB](../../integration-services/data-flow/ole-db-source.md)     
 [Destinazione OLE DB](../../integration-services/data-flow/ole-db-destination.md)     
 [Attività Esegui SQL](../../integration-services/control-flow/execute-sql-task.md)     
 [Connessioni in Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)    
    
  
