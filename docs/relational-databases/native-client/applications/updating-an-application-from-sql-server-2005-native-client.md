---
title: Native client, aggiornare l'app SQL 2005
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, updating applications
ms.assetid: 1e1e570c-7f14-4e16-beab-c328e3fbdaa8
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2eddd2284ec77a1a4979389f964baeafb6932dc5
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243805"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>Aggiornamento di un'applicazione da SQL Server 2005 Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In questo argomento vengono descritte le modifiche di rilievo introdotte in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client rispetto a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Quando si esegue l'aggiornamento da Microsoft Data Access Components (MDAC) a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, si potrebbero anche notare alcune differenze di comportamento. Per ulteriori informazioni, vedere [aggiornamento di un'applicazione a SQL Server Native Client da MDAC](../../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 fornito con [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 fornito con [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 fornito con [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 fornito con [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)].  
  
|Differenze di comportamento in SQL Server Native Client nelle versione successive a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]|Description|  
|------------------------------------------------------------------------------------|-----------------|  
|In OLE DB viene applicato il riempimento solo in base alla scala definita.|Per le conversioni in cui i dati convertiti vengono inviati al [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] server, Native Client ( [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]a partire da) assorbe gli zeri finali nei dati solo fino alla lunghezza massima dei valori **DateTime** . In SQL Server Native Client 9.0 viene applicato un riempimento fino a un massimo di 9 cifre.|  
|Convalidare DBTYPE_DBTIMESTAMP per ICommandWithParameter:: separameterinfo.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client (a partire [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]da) implementa il requisito OLE DB per *bScale* in ICommandWithParameter:: separameterinfo da impostare sulla precisione frazionaria dei secondi per DBTYPE_DBTIMESTAMP.|  
|Il **sp_columns** stored procedure ora restituisce **"No"** invece di **"no"** per la colonna IS_NULLABLE.|A [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] partire da Native Client 10,0[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)](), **sp_columns** stored procedure ora restituisce **"No"** invece di **"No"** per una colonna IS_NULLABLE.|  
|SQLSetDescRec, SQLBindParameter e SQLBindCol eseguono ora la verifica della coerenza.|Prima di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10,0, l'impostazione SQL_DESC_DATA_PTR non ha provocato una verifica di coerenza per qualsiasi tipo di descrittore in SQLSetDescRec, SQLBindParameter o SQLBindCol.|  
|SQLCopyDesc ora esegue la verifica della coerenza del descrittore.|Prima di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10,0, SQLCopyDesc non esegue una verifica di coerenza quando il campo SQL_DESC_DATA_PTR è stato impostato su un record specifico.|  
|SQLGetDescRec non esegue più una verifica di coerenza del descrittore.|Prima di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10,0, SQLGetDescRec esegue una verifica di coerenza del descrittore quando è stato impostato il campo SQL_DESC_DATA_PTR. Tale controllo non è richiesto dalla specifica ODBC e in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) e versioni successive non viene più eseguito.|  
|Quando la data non è inclusa nell'intervallo consentito viene restituito un errore differente.|Per il tipo **DateTime** , un numero di errore diverso verrà restituito da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]partire da) per una data non compresa nell'intervallo rispetto a quello restituito nelle versioni precedenti.<br /><br /> In particolare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , native client 9,0 ha restituito 22007 per tutti i valori di anno fuori intervallo nelle conversioni di stringa in **DateTime**e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] native client a partire dalla[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]versione 10,0 () restituisce 22008 quando la data rientra nell'intervallo supportato da **datetime2** ma non compreso nell'intervallo supportato da **DateTime** o **smalldatetime**.|  
|il valore **DateTime** tronca i secondi frazionari e non arrotonda se l'arrotondamento cambierà il giorno.|Nelle versioni precedenti a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, il client arrotonda i valori **datetime** inviati al server al valore più vicino corrispondente a 1/300 di secondo. A partire da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, in questo scenario si verifica il troncamento dei secondi frazionari se l'arrotondamento comporta la modifica del giorno.|  
|Possibile troncamento di secondi per il valore **DateTime** .|In un'applicazione compilata con [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (o versioni successive) che si connette a un server [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 vengono troncati i secondi e i secondi frazionari per la porzione di tempo dei dati inviati al server se si esegue l'associazione a una colonna datetime con un identificatore di tipo DBTYPE_DBTIMESTAMP (OLE DB) o SQL_TIMESTAMP (ODBC) e una scala di 0.<br /><br /> Ad esempio:<br /><br /> Dati di input: 1994-08-21 21:21:36.000<br /><br /> Dati inseriti: 1994-08-21 21:21:00.000|  
|La conversione dei dati OLE DB da DBTYPE_DBTIME a DBTYPE_DATE non può più causare la modifica del giorno.|Nelle versioni precedenti a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, se la parte relativa all'ora di un tipo DBTYPE_DATE è entro mezzo secondo dalla mezzanotte, il codice di conversione OLE DB causa la modifica del giorno. A partire da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, il giorno non viene modificato (i secondi frazionari vengono troncati ma non vengono arrotondati).|  
|Modifiche della conversione IBCPSession:: BCColFmt.|A partire [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da Native Client 10,0, quando si usa IBCPSession:: BCOColFmt per convertire SQLDATETIME o SqlDateTime in un tipo stringa, viene esportato un valore frazionario. Quando ad esempio si converte il tipo SQLDATETIME nel tipo SQLNVARCHARMAX, le versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client restituiscono<br /><br /> 1989-02-01 00:00:00. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 e versioni successive restituiscono 1989-02-01 00:00:00.0000000.|  
|Le dimensioni dei dati inviati devono corrispondere alla lunghezza specificata in SQL_LEN_DATA_AT_EXEC.|Quando si utilizza SQL_LEN_DATA_AT_EXEC, le dimensioni dei dati devono corrispondere alla lunghezza specificata con SQL_LEN_DATA_AT_EXEC. È possibile utilizzare SQL_DATA_AT_EXEC ma l'utilizzo di SQL_LEN_DATA_AT_EXEC comporta vantaggi potenziali in termini di prestazioni.|  
|Le applicazioni personalizzate che utilizzano l'API BCP ora possono visualizzare un avviso.|L'API BCP genererà un messaggio di avviso se la lunghezza dei dati di tutti i tipi è superiore a quella specificata per un campo. In precedenza, questo avviso veniva visualizzato solo per i dati di tipo carattere e non per tutti i tipi.|  
|Se si inserisce una stringa vuota in una colonna **sql_variant** associata come tipo data/ora, viene generato un errore.|In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 l'inserimento di una stringa vuota in una colonna **sql_variant** associata come tipo data/ora non generava alcun errore. In questa situazione in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 e versioni successive viene correttamente generato un errore.|  
|Convalida dei parametri SQL_C_TYPE _TIMESTAMP e DBTYPE_DBTIMESTAMP più restrittiva.|Prima di [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] native client, i valori **DateTime** venivano arrotondati per adattarsi alla scala delle colonne **DateTime** e **smalldatetime** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. 
  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (e versioni successive) applica le regole di convalida più restrittive definite nella specifica ODBC per i secondi frazionari. Se non è possibile convertire il valore di un parametro nel tipo SQL utilizzando la scala specificata o implicita dell'associazione client senza causare il troncamento delle cifre finali, viene restituito un errore.|  
|Quando è in esecuzione un trigger, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] potrebbe restituire risultati diversi.|A causa delle modifiche introdotte in [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], un'istruzione che ha causato l'esecuzione di un trigger con **NOCOUNT OFF** attivo potrebbe restituire a un'applicazione risultati diversi. In una situazione di questo tipo l'applicazione potrebbe generare un errore. Per correggere l'errore, impostare **NOCOUNT ON** nel trigger o chiamare SQLMoreResults per passare al risultato successivo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione in SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
