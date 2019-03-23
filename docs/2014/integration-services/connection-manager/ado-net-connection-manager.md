---
title: Gestione connessione ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 97a0690775b7b6d95a257bc5f5ed0a6483e1c24a
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58380299"
---
# <a name="adonet-connection-manager"></a>Gestione connessione ADO.NET
  Una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] consente l'accesso di un pacchetto alle origini dati tramite un provider .NET. Questa gestione connessione viene di solito usata per accedere a origini dati quali [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nonché a origini dati esposte tramite OLE DB e XML in attività personalizzate scritte in codice gestito, usando un linguaggio come C#.  
  
 Quando si aggiunge un [!INCLUDE[vstecado](../../includes/vstecado-md.md)] gestione connessione a un pacchetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una connessione di gestione che viene risolto come un [!INCLUDE[vstecado](../../includes/vstecado-md.md)] connessione in fase di esecuzione, imposta le proprietà di gestione connessione e aggiunge la gestione connessione il `Connections` raccolta nel pacchetto.  
  
 La proprietà `ConnectionManagerType` della gestione connessione viene impostata su `ADO.NET`. Il valore di `ConnectionManagerType` è qualificato con il nome del provider .NET utilizzato dalla gestione connessione.  
  
## <a name="adonet-connection-manager-troubleshooting"></a>Risoluzione dei problemi relativi alla gestione connessione ADO.NET  
 È possibile registrare le chiamate eseguite dalla gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a provider di dati esterni. Questa nuova funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi alle connessioni stabilite dalla gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a origini dati esterne. Per registrare le chiamate eseguite dalla gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a provider di dati esterni, abilitare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** a livello di pacchetto. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 Durante la lettura da parte di una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , i dati di alcuni tipi di dati date di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genereranno i risultati mostrati nella tabella seguente.  
  
|Tipo di dati di SQL Server|Risultato|  
|--------------------------|------------|  
|`time`, `datetimeoffset`|L'esecuzione del pacchetto non viene completata correttamente, a meno che non vengano utilizzati comandi SQL con parametri. È necessario servirsi dell'attività Esegui SQL nel pacchetto per utilizzare i comandi SQL con parametri. Per altre informazioni, vedere [Attività Esegui SQL](../control-flow/execute-sql-task.md) e [Parametri e codici restituiti nell'attività Esegui SQL](../parameters-and-return-codes-in-the-execute-sql-task.md).|  
|`datetime2`|La gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] tronca il valore relativo ai millisecondi.|  
  
> [!NOTE]  
>  Per altre informazioni sui tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e sul relativo mapping nei tipi di dati [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Tipi di dati &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) e [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).  
  
## <a name="adonet-connection-manager-configuration"></a>Configurazione della gestione connessione ADO.NET  
 Per configurare una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , procedere nel modo seguente:  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
-   Specificare una stringa di connessione configurata in modo da soddisfare i requisiti del provider .NET selezionato.  
  
-   Se richiesto dal provider, includere il nome dell'origine dei dati a cui connettersi.  
  
-   Specificare le credenziali di sicurezza come previsto dal provider selezionato.  
  
-   Indicare se la connessione creata dalla gestione connessione deve essere mantenuta in fase di esecuzione.  
  
 Molte delle opzioni di configurazione della gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] dipendono dal provider .NET usato dalla gestione connessione.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Configura gestione connessione ADO.NET](../configure-ado-net-connection-manager.md)  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Connessioni in Integration Services &#40;SSIS&#41;](integration-services-ssis-connections.md)  
  
  
