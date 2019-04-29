---
title: SQLBrowseConnect | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBrowseConnect function
ms.assetid: 57faf388-c7ca-4696-9845-34e0a10cc5f7
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 32741a2efaa3d7903c45d978c72f1ccc6867b1ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63014733"
---
# <a name="sqlbrowseconnect"></a>SQLBrowseConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLBrowseConnect** utilizza le parole chiave che possono essere suddivise in tre livelli di informazioni di connessione. Per ogni parola chiave nella tabella seguente è indicato se viene restituito un elenco di valori validi e se la parola chiave è facoltativa.  
  
## <a name="level-1"></a>Livello 1  
  
|Parola chiave|Elenco restituito?|Facoltativa?|Descrizione|  
|-------------|--------------------|---------------|-----------------|  
|DSN|N/D|No|Nome dell'origine dati restituiti da **SQLDataSources**. Se viene utilizzata la parola chiave DRIVER, non è possibile utilizzare la parola chiave DSN.|  
|DRIVER|N/D|No|Microsoft® [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome del driver ODBC Native Client è {[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 11 Client nativo}. Se viene utilizzata la parola chiave DSN, non è possibile utilizzare la parola chiave DRIVER.|  
  
## <a name="level-2"></a>Livello 2  
  
|Parola chiave|Elenco restituito?|Facoltativa?|Descrizione|  
|-------------|--------------------|---------------|-----------------|  
|SERVER|Yes|No|Nome del server in rete nel quale risiede l'origine dati. È consentita la specifica del termine "(local)" per indicare il server. In questo caso, è possibile utilizzare una copia locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], anche quando si tratta di una versione non in rete.|  
|UID|No|Yes|ID di accesso dell'utente.|  
|PWD|No|Sì (dipende dall'utente)|Password specificata dall'utente.|  
|APP|No|Yes|Nome della chiamata al metodo di applicazione **SQLBrowseConnect**.|  
|WSID|No|Yes|ID della workstation. In genere, si tratta del nome di rete del computer sul quale viene eseguita l'applicazione.|  
  
## <a name="level-3"></a>Livello 3  
  
|Parola chiave|Elenco restituito?|Facoltativa?|Descrizione|  
|-------------|--------------------|---------------|-----------------|  
|DATABASE|Yes|Yes|Nome del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|LANGUAGE|Yes|Yes|Lingua nazionale utilizzata in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
 **SQLBrowseConnect** ignora i valori delle parole chiave del DATABASE e della lingua memorizzate nelle definizioni delle origini dati ODBC. Se il database o la lingua specificata nella stringa di connessione passata a **SQLBrowseConnect** non è valido **SQLBrowseConnect** restituisce SQL_NEED_DATA e gli attributi di connessione di livello 3.  
  
 I seguenti attributi, vengono impostati tramite la chiamata [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), determinare il set di risultati restituito da **SQLBrowseConnect**.  
  
|attribute|Descrizione|  
|---------------|-----------------|  
|SQL_COPT_SS_BROWSE_CONNECT|Se è impostato su SQL_MORE_INFO_YES, **SQLBrowseConnect** restituisce una stringa estesa delle proprietà del server.<br /><br /> Di seguito è riportato un esempio di una stringa estesa restituito da **SQLBrowseConnect**:<br /><br /> <br /><br /> `ServerName\InstanceName;Clustered:No;Version:8.00.131`<br /><br /> <br /><br /> In questa stringa i punti e virgola separano le diverse informazioni sul server. Le virgole separano le diverse istanze del server.|  
|SQL_COPT_SS_BROWSE_SERVER|Se viene specificato un nome di server, **SQLBrowseConnect** restituirà informazioni per il server specificato. Se SQL_COPT_SS_BROWSE_SERVER è impostato su NULL, **SQLBrowseConnect** restituisce informazioni per tutti i server nel dominio.<br /><br /> <br /><br /> Si noti che a causa di problemi di rete, **SQLBrowseConnect** potrebbe non ricevere una risposta tempestiva da tutti i server. L'elenco di server restituito può pertanto variare per ogni richiesta.|  
|SQL_COPT_SS_BROWSE_CACHE_DATA|Quando l'attributo SQL_COPT_SS_BROWSE_CACHE_DATA è impostato su SQL_CACHE_DATA_YES, è possibile recuperare i dati in blocchi quando la lunghezza del buffer non è sufficiente per contenere il risultato. Questa lunghezza è specificata nell'argomento BufferLength SQLBrowseConnect.<br /><br /> Quando sono disponibili più dati, viene restituito SQL_NEED_DATA. Quando non vi sono più dati da recuperare, viene restituito SQL_SUCCESS.<br /><br /> Il valore predefinito è SQL_CACHE_DATA_NO.|  
  
## <a name="sqlbrowseconnect-support-for-high-availability-disaster-recovery"></a>Supporto di SQLBrowseConnect per il ripristino di emergenza a disponibilità elevata  
 Per ulteriori informazioni sull'utilizzo di **SQLBrowseConnect** per la connessione a un [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] cluster, vedere [SQL Server Native Client supporto disponibilità elevata e ripristino di emergenza](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
## <a name="sqlbrowseconnect-support-for-service-principal-names-spns"></a>Supporto di SQLBrowseConnect per i nomi SPN (Service Principal Name)  
 Quando si apre una connessione, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client imposta SQL_COPT_SS_MUTUALLY_AUTHENTICATED e SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD sul metodo di autenticazione utilizzato per aprire la connessione.  
  
 Per altre informazioni sui nomi SPN, vedere [nomi delle entità servizio &#40;SPN&#41; nelle connessioni Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="change-history"></a>Cronologia modifiche  
  
|Contenuto aggiornato|  
|---------------------|  
|Informazioni su SQL_COPT_SS_BROWSE_CACHE_DATA.|  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLBrowseConnect](https://go.microsoft.com/fwlink/?LinkId=59329)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
