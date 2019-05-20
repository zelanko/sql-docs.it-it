---
title: Gestione connessione ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetconnection.f1
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b4078c1b6bea837ae7f5f9b1ffc9529076660059
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728417"
---
# <a name="adonet-connection-manager"></a>Gestione connessione ADO.NET

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] consente l'accesso di un pacchetto alle origini dati tramite un provider .NET. Questa gestione connessione viene di solito usata per accedere a origini dati quali [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nonché a origini dati esposte tramite OLE DB e XML in attività personalizzate scritte in codice gestito, usando un linguaggio come C#.  
  
 Quando si aggiunge una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a un pacchetto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , imposta le proprietà della gestione connessione, quindi aggiunge quest'ultima alla raccolta delle **connessioni** del pacchetto.  
  
 La proprietà **ConnectionManagerType** della gestione connessione viene impostata su **ADO.NET**. Il valore di **ConnectionManagerType** è qualificato con il nome del provider .NET usato dalla gestione connessione.  
  
## <a name="adonet-connection-manager-troubleshooting"></a>Risoluzione dei problemi relativi alla gestione connessione ADO.NET  
 È possibile registrare le chiamate eseguite dalla gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a provider di dati esterni. Questa nuova funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi alle connessioni stabilite dalla gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a origini dati esterne. Per registrare le chiamate eseguite dalla gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a provider di dati esterni, abilitare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** a livello di pacchetto. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 Durante la lettura da parte di una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , i dati di alcuni tipi di dati date di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genereranno i risultati mostrati nella tabella seguente.  
  
|Tipo di dati di SQL Server|Risultato|  
|--------------------------|------------|  
|**time**, **datetimeoffset**|L'esecuzione del pacchetto non viene completata correttamente, a meno che non vengano utilizzati comandi SQL con parametri. È necessario servirsi dell'attività Esegui SQL nel pacchetto per utilizzare i comandi SQL con parametri. Per altre informazioni, vedere [Attività Esegui SQL](../../integration-services/control-flow/execute-sql-task.md) e [Parametri e codici restituiti nell'attività Esegui SQL](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).|  
|**datetime2**|La gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] tronca il valore relativo ai millisecondi.|  
  
> [!NOTE]  
>  Per altre informazioni sui tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e sul relativo mapping nei tipi di dati [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) e [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="adonet-connection-manager-configuration"></a>Configurazione della gestione connessione ADO.NET  
 Per configurare una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , procedere nel modo seguente:  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
-   Specificare una stringa di connessione configurata in modo da soddisfare i requisiti del provider .NET selezionato.  
  
-   Se richiesto dal provider, includere il nome dell'origine dei dati a cui connettersi.  
  
-   Specificare le credenziali di sicurezza come previsto dal provider selezionato.  
  
-   Indicare se la connessione creata dalla gestione connessione deve essere mantenuta in fase di esecuzione.  
  
 Molte delle opzioni di configurazione della gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] dipendono dal provider .NET usato dalla gestione connessione.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Configura gestione connessione ADO.NET](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="configure-adonet-connection-manager"></a>Configura gestione connessione ADO.NET
  Utilizzare la finestra di dialogo **Configura gestione connessione ADO.NET** per aggiungere una connessione a un'origine dati accessibile mediante un provider di dati .NET Framework, ad esempio il provider SqlClient. La gestione connessione può utilizzare una connessione esistente oppure è possibile crearne una nuova.  
  
 Per ulteriori informazioni sulla gestione connessione ADO.NET, vedere [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Connessioni dati**  
 Consente di selezionare una connessione dati ADO.NET esistente nell'elenco.  
  
 **Proprietà connessione dati**  
 Consente di visualizzare proprietà e valori per la connessione dati ADO.NET selezionata.  
  
 **Nuova**  
 Consente di creare una connessione dati ADO.NET tramite la finestra di dialogo **Gestione connessione** .  
  
 **Elimina**  
 Selezionare una connessione e quindi eliminarla utilizzando il pulsante **Elimina** .  
  
## <a name="see-also"></a>Vedere anche  
 [Connessioni in Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
