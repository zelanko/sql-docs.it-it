---
title: Gestione connessione ADO | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], ADO
- connection managers [Integration Services], ADO
- ADO connection manager [Integration Services]
ms.assetid: 490418bc-5ef1-41b8-a9c8-de38aa96e0f6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a9fdbe8cca12779e6666e0305ddfb081f3649f44
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294470"
---
# <a name="ado-connection-manager"></a>Gestione connessione ADO

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Una gestione connessione ADO consente la connessione di un pacchetto a oggetti ADO (ActiveX Data Objects), ad esempio un recordset. Questa gestione connessione viene in genere usata nelle attività personalizzate create con versioni precedenti di un linguaggio, ad esempio Microsoft Visual Basic 6.0, o in attività personalizzate che fanno parte di un'applicazione esistente che usa ADO per connettersi a un'origine dei dati.  
  
 Quando si aggiunge una gestione connessione ADO a un pacchetto, in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene creata una gestione connessione che in fase di esecuzione verrà risolta in una connessione ADO, vengono impostate le proprietà della gestione connessione, dopodiché la gestione connessione viene aggiunta alla raccolta **Connections** del pacchetto. La proprietà **ConnectionManagerType** della gestione connessione viene impostata su **ADO**.  
  
## <a name="troubleshooting-the-ado-connection-manager"></a>Risoluzione dei problemi relativi alla gestione connessione ADO  
 Durante la lettura da parte di una gestione connessione ADO, alcuni tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relativi alle date genereranno i risultati mostrati nella tabella seguente.  
  
|Tipo di dati di SQL Server|Risultato|  
|--------------------------|------------|  
|**time**, **datetimeoffset**|L'esecuzione del pacchetto non viene completata correttamente, a meno che non vengano utilizzati comandi SQL con parametri. È necessario servirsi dell'attività Esegui SQL nel pacchetto per utilizzare i comandi SQL con parametri. Per altre informazioni, vedere [Attività Esegui SQL](../../integration-services/control-flow/execute-sql-task.md) e [Parametri e codici restituiti nell'attività Esegui SQL](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).|  
|**datetime2**|La gestione connessione ADO tronca il valore relativo ai millisecondi.|  
  
> [!NOTE]  
>  Per altre informazioni sui tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e sul relativo mapping nei tipi di dati [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) e [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="configuring-the-ado-connection-manager"></a>Configurazione della gestione connessione ADO  
 Per configurare una gestione connessione ADO, procedere nel modo seguente:  
  
-   Specificare una stringa di connessione configurata in modo da soddisfare i requisiti del provider selezionato.  
  
-   Se richiesto dal provider, includere il nome dell'origine dei dati a cui connettersi.  
  
-   Specificare le credenziali di sicurezza come previsto dal provider selezionato.  
  
-   Indicare se la connessione creata dalla gestione connessione deve essere mantenuta in fase di esecuzione.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Configura gestione connessione OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Connessioni in Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
