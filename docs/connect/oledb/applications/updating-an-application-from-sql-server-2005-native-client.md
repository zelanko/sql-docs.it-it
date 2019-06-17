---
title: Aggiornamento di un'applicazione da SQL Server 2005 Native Client | Microsoft Docs
description: Aggiornamento di un'applicazione da SQL Server 2005 Native Client
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 17280079f493d8abbad2f8ffb76d25c2a0ba868f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66771073"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>Aggiornamento di un'applicazione da SQL Server 2005 Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Questo argomento illustra le modifiche di rilievo nel Driver OLE DB per SQL Server poiché [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

 Quando si esegue l'aggiornamento da Microsoft Data Access Components (MDAC) al driver OLE DB per SQL Server, si possono anche notare alcune differenze di comportamento. Per altre informazioni, vedere [aggiornamento di un'applicazione al Driver OLE DB per SQL Server da MDAC](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 fornito con [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 fornito con [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 fornito con [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 fornito con [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)].  

|Modificare il comportamento nel Driver OLE DB per SQL Server rispetto a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client|Descrizione|  
|------------------------------------------------------------------------------------|-----------------|  
|In OLE DB viene applicato il riempimento solo in base alla scala definita.|Per le conversioni in cui i dati convertiti vengono inviati al server, il Driver OLE DB per SQL Server inserisce zeri finali nei dati solo fino alla lunghezza massima dei **datetime** valori. In SQL Server Native Client 9.0 viene applicato un riempimento fino a un massimo di 9 cifre.|  
|Convalida di DBTYPE_DBTIMESTAMP per ICommandWithParameter::SetParameterInfo.|Driver OLE DB per SQL Server implementa il requisito OLE DB per *bScale* in ICommandWithParameter::SetParameterInfo da impostare per la precisione secondi frazionari per DBTYPE_DBTIMESTAMP.|  
|Il **sp_columns** stored procedure restituisce ora **"NO"** anziché **"NO"** per la colonna IS_NULLABLE.|Nel Driver OLE DB per SQL Server, **sp_columns** stored procedure restituisce ora **"NO"** anziché **"NO"** per una colonna IS_NULLABLE.|  
|Quando la data non è inclusa nell'intervallo consentito viene restituito un errore differente.|Per il **datetime** tipo, un numero di errore diversi restituirà Driver OLE DB per SQL Server per una data di out-of-range quello restituito nelle versioni precedenti.<br /><br /> In particolare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 restituiva il numero 22007 per tutti i valori fuori intervallo anno nelle conversioni di stringa per **datetime**, e il Driver OLE DB per SQL Server restituisce il numero 22008 quando la data è compresa nell'intervallo supportato dal **datetime2** ma esterna all'intervallo supportato da **datetime** oppure **smalldatetime**.|  
|Il valore **datetime** tronca i secondi frazionari e non viene arrotondato se tale arrotondamento comporta la modifica del giorno.|Nelle versioni precedenti a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, il client arrotonda i valori **datetime** inviati al server al valore più vicino corrispondente a 1/300 di secondo. Nel Driver OLE DB per SQL Server, questo scenario causa il troncamento dei secondi frazionari se l'arrotondamento comporta la modifica del giorno.|  
|Possibile troncamento di secondi per **datetime** valore.|In un'applicazione compilata con il driver OLE DB per SQL Server che si connette a un server [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 vengono troncati i secondi e i secondi frazionari per la porzione relativa al tempo dei dati inviati al server se si esegue l'associazione a una colonna datetime con un identificatore di tipo DBTYPE_DBTIMESTAMP (OLE DB) o SQL_TIMESTAMP (ODBC) e una scala di 0.<br /><br /> Esempio:<br /><br /> Dati di input: 1994-08-21 21:21:36.000<br /><br /> Dati inseriti: 1994-08-21 21:21:00.000|  
|La conversione dei dati OLE DB da DBTYPE_DBTIME a DBTYPE_DATE non può più causare la modifica del giorno.|Nelle versioni precedenti a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, se la parte relativa all'ora di un tipo DBTYPE_DATE è entro mezzo secondo dalla mezzanotte, il codice di conversione OLE DB causa la modifica del giorno. Nel Driver OLE DB per SQL Server, il giorno non viene modificato (i secondi frazionari vengono troncati e non vengono arrotondati).|  
|Modifiche relative alle conversioni IBCPSession::BCColFmt.|Nel Driver OLE DB per SQL Server, quando si usa IBCPSession::BCOColFmt per convertire SQLDATETIME o SQLDATETIME in un tipo stringa, viene esportato un valore frazionario. Se ad esempio si converte il tipo SQLDATETIME nel tipo SQLNVARCHARMAX, le versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 restituiscono<br /> 1989-02-01 00:00:00.<br />Il driver OLE DB per SQL Server restituisce <br />1989-02-01 00:00:00.0000000.|  
|Le applicazioni personalizzate che utilizzano l'API BCP ora possono visualizzare un avviso.|L'API BCP genererà un messaggio di avviso se la lunghezza dei dati di tutti i tipi è superiore a quella specificata per un campo. In precedenza, questo avviso veniva visualizzato solo per i dati di tipo carattere e non per tutti i tipi.|  
|Se si inserisce una stringa vuota in una colonna **sql_variant** associata come tipo data/ora, viene generato un errore.|In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 l'inserimento di una stringa vuota in una colonna **sql_variant** associata come tipo data/ora non generava alcun errore. In questo caso, il Driver OLE DB per SQL Server genera correttamente un errore.|  
|Quando è in esecuzione un trigger, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] potrebbe restituire risultati diversi.|A causa delle modifiche introdotte in [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], un'istruzione che ha causato l'esecuzione di un trigger con **NOCOUNT OFF** attivo potrebbe restituire a un'applicazione risultati diversi. In una situazione di questo tipo l'applicazione potrebbe generare un errore. Per risolvere questo problema, impostare **NOCOUNT ON** nel trigger.|  

## <a name="see-also"></a>Vedere anche   
 [Driver OLE DB per SQL Server](../../oledb/oledb-driver-for-sql-server.md)
