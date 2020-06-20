---
title: Uso di gestioni connessioni a livello di programmazione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- connection managers [Integration Services], programming
ms.assetid: 2686fe84-1ecc-48b8-9160-e7122274bd84
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6053418c624c2ab107a35a02c382576dcb41a534
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972441"
---
# <a name="working-with-connection-managers-programmatically"></a>Utilizzo di gestioni connessioni a livello di programmazione
  In [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] il metodo AcquireConnection della classe della gestione connessione associata è quello che viene chiamato più spesso quando si usano gestioni connessioni in codice gestito. Quando si scrive codice gestito, è necessario chiamare il metodo AcquireConnection per usare la funzionalità di una gestione connessione. È necessario chiamare questo metodo sia che il codice gestito venga scritto in un'attività Script, in un componente script, in un oggetto personalizzato o in un'applicazione personalizzata.  
  
 Per chiamare correttamente il metodo AcquireConnection, è necessario conoscere le risposte alle domande seguenti:  
  
-   **Quali gestioni connessioni restituiscono un oggetto gestito dal metodo AcquireConnection?**  
  
     Molte gestioni connessioni restituiscono oggetti COM non gestiti (System.__ComObject), che non possono essere facilmente usati da codice gestito. L'elenco di queste gestioni connessioni include la gestione connessione OLE DB utilizzata di frequente.  
  
-   **Per le gestioni connessioni che restituiscono un oggetto gestito, quali oggetti vengono restituiti dai relativi metodi AcquireConnection?**  
  
     Per eseguire il cast del valore restituito nel tipo appropriato, è necessario conoscere il tipo di oggetto restituito dal metodo AcquireConnection. Ad esempio, il metodo AcquireConnection per la gestione connessione [!INCLUDE[vstecado](../includes/vstecado-md.md)] restituisce un oggetto SqlConnection aperto quando si usa il provider SqlClient. Tuttavia, il metodo AcquireConnection per la gestione connessione file restituisce solo una stringa.  
  
 In questo argomento vengono fornite le risposte a queste domande per le gestioni connessioni incluse in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
## <a name="connection-managers-that-do-not-return-a-managed-object"></a>Gestioni connessione che non restituiscono un oggetto gestito  
 La tabella seguente elenca le gestioni connessioni che restituiscono un oggetto COM nativo (System.__ComObject) dal metodo AcquireConnection. Tali oggetti non gestiti non possono essere facilmente utilizzati da codice gestito.  
  
|Tipo di gestione connessione|Nome gestione connessione|  
|-----------------------------|-----------------------------|  
|ADO|Gestione connessione ADO|  
|MSOLAP90|Gestione connessione [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|  
|EXCEL|Gestione connessione Excel|  
|FTP|gestione connessione FTP|  
|HTTP|gestione connessione HTTP|  
|ODBC|gestione connessione ODBC|  
|OLEDB|gestione connessione OLE DB|  
  
 In genere, è possibile usare una gestione connessione [!INCLUDE[vstecado](../includes/vstecado-md.md)] da codice gestito per connettersi a un'origine dati ADO, Excel, ODBC o OLE DB.  
  
## <a name="return-values-from-the-acquireconnection-method"></a>Valori restituiti dal metodo AcquireConnection  
 La tabella seguente elenca le gestioni connessioni che restituiscono un oggetto gestito dal metodo AcquireConnection. Tali oggetti gestiti possono essere facilmente utilizzati da codice gestito.  
  
|Tipo di gestione connessione|Nome gestione connessione|Tipo di valore restituito|Informazioni aggiuntive|  
|-----------------------------|-----------------------------|--------------------------|----------------------------|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|Gestione connessione [!INCLUDE[vstecado](../includes/vstecado-md.md)]|`System.Data.SqlClient.SqlConnection`||  
|FILE|gestione connessione file|`System.String`|Percorso del file.|  
|FLATFILE|Flat File Connection Manager|`System.String`|Percorso del file.|  
|MSMQ|gestione connessione MSMQ|`System.Messaging.MessageQueue`||  
|MULTIFILE|gestione connessione per più file|`System.String`|Percorso di uno dei file.|  
|MULTIFLATFILE|gestione connessione per più file flat|`System.String`|Percorso di uno dei file.|  
|SMOServer|gestione connessione SMO|`Microsoft.SqlServer.Management.Smo.Server`||  
|SMTP|Gestione connessione SMTP|`System.String`|ad esempio `SmtpServer=<server name>;UseWindowsAuthentication=True;EnableSsl=False;`|  
|WMI|Gestione connessione WMI|`System.Management.ManagementScope`||  
|SQLMOBILE|Gestione connessione SQL Server Compact|`System.Data.SqlServerCe.SqlCeConnection`||  
  
![Integration Services icona (piccola)](media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visitare la pagina relativa a Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Connessione alle origini dati nell'attività script](extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)   
 [Connessione a origini dati nel componente script](extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)   
 [Connessione alle origini dati in un'attività personalizzata](extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
  
  
