---
title: sys.bandwidth_usage (database SQL di Azure) Documenti Microsoft
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- bandwidth_usage
- sys.bandwidth_usage
- bandwidth_usage_TSQL
- sys.bandwidth_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.bandwidth_usage
- bandwidth_usage
ms.assetid: 43ed8435-f059-4907-b5c0-193a258b394a
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: ea963c07a15cd5c2db3cca113680026d3100936b
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2020
ms.locfileid: "67942571"
---
# <a name="sysbandwidth_usage-azure-sql-database"></a>sys.bandwidth_usage (Azure SQL Database)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

> [!NOTE]
> Questo vale [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]solo per V11.  
  
 Restituisce informazioni sulla larghezza di banda di rete utilizzata da ogni database in un ** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] server di database V11,**. In ogni riga restituita per un determinato database vengono riepilogate una direzione e una classe di utilizzo per un periodo di un'ora.  
  
 **Questo è stato deprecato in un [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]file .**  
  
 La vista **sys.bandwidth_usage** contiene le colonne seguenti.  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|**time**|Ora in cui la larghezza di banda è stata usata. Le righe di questa vista hanno base oraria. Ad esempio, 2009-09-19 02:00:00.000 indica che la larghezza di banda è stata usata il 19 settembre 2009 tra le 14.00 e le 3.00.|  
|**database_name**|Nome del database che ha usato la larghezza di banda.|  
|**direction**|Tipo di larghezza di banda usata, uno di:<br /><br /> Ingresso: dati che si [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]spostano nel file .<br /><br /> Uscita: dati che si spostano all'esterno [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]del file .|  
|**classe**|Classe di larghezza di banda usata, una di:<br />Interno: dati in movimento all'interno della piattaforma Azure.Internal: Data that is moving within the Azure platform.<br />Esterno: dati che si spostano dalla piattaforma Azure.External: Data that is moving out of the Azure platform.<br /><br /> Questa classe viene restituita solo se il database è occupato in una relazione di copia continua tra aree ([!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]). Se un determinato database non partecipa ad alcuna relazione di copia continua, le righe "Interlink" non vengono restituite. Per ulteriori informazioni, vedere la sezione "Osservazioni" di seguito in questo argomento.|  
|**time_period**|Il periodo di tempo in cui si è verificato l'utilizzo è Peak o OffPeak. L'ora Peak si basa sull'area geografica in cui è stato creato il server. Ad esempio, se un server è stato creato nell'area geografica "US_Northwest", l'ora Peak è compresa tra le 10.00 e le 18.00 PST.|  
|**quantity**|La quantità di larghezza di banda, in kilobyte (KB), usata.|  
  
## <a name="permissions"></a>Autorizzazioni

 Questa visualizzazione è disponibile solo nel database **master** per l'account di accesso dell'entità a livello di server.  
  
## <a name="remarks"></a>Osservazioni  
  
### <a name="external-and-internal-classes"></a>Classi External e Internal

 Per ogni database utilizzato in un determinato momento, la visualizzazione **sys.bandwidth_usage** restituisce le righe che mostrano la classe e la direzione dell'utilizzo della larghezza di banda. Nell'esempio seguente vengono illustrati i dati che possono essere esposti per un determinato database. In questo esempio, la data e l'ora sono 2012-04-21 17:00:00, che cade nel periodo di massima attività. Il nome del database è Db1. In questo esempio, **sys.bandwidth_usage** ha restituito una riga per tutte e quattro le combinazioni delle direzioni di ingresso e uscita e delle classi esterne e interne, come indicato di seguito:  
  
|time|database_name|direction|classe|time_period|quantity|  
|----------|--------------------|---------------|-----------|------------------|--------------|  
|2012-04-21 17:00:00|Db1|Dati in ingresso|Esterno|Peak|66|  
|2012-04-21 17:00:00|Db1|Egress|Esterno|Peak|741|  
|2012-04-21 17:00:00|Db1|Dati in ingresso|Interno|Peak|1052|  
|2012-04-21 17:00:00|Db1|Egress|Interno|Peak|3525|  
  
### <a name="interpreting-data-direction-for-ssgeodr"></a>Interpretazione della direzione dati per [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]

 Per la [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)], i dati di utilizzo della larghezza di banda sono visibili nel database master logico da entrambi i lati di una relazione di copia continua. Quindi è necessario interpretare gli indicatori di direzione di ingresso e di uscita dal punto di vista dei database su cui si sta sucpersonando. Ad esempio, considerare un flusso di replica che trasferisce 1 MB di dati dal server di origine al server di destinazione. In questo caso, nel server di origine, il MB viene conteggiato nel totale dei dati inviati mentre nel server di destinazione, il MB viene registrato come dati ricevuti.  
  
> [!NOTE]  
> Il bulk dei dati vengono trasferiti dal server di origine al server di destinazione, nella direzione del flusso dei dati utente. Tuttavia, parte del trasferimento dei dati viene richiesto nell'altra direzione.  
