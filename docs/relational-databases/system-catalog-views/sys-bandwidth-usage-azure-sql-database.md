---
title: Sys. bandwidth_usage (Database SQL di Azure) | Microsoft Docs
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
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 4b7534a806a856dee922ead1055da6a7567a4d8c
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716597"
---
# <a name="sysbandwidthusage-azure-sql-database"></a>sys.bandwidth_usage (Azure SQL Database)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

> [!NOTE]
> Si applica solo al [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11.* *  
  
 Restituisce informazioni sulla larghezza di banda di rete utilizzata da ogni database in un  **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] server di database V11**,. In ogni riga restituita per un determinato database vengono riepilogate una direzione e una classe di utilizzo per un periodo di un'ora.  
  
 **Questa è stata deprecata in una [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].**  
  
 Il **Sys. bandwidth_usage** vista contiene le colonne seguenti.  
  
|Column Name|Descrizione|  
|-----------------|-----------------|  
|**time**|Ora in cui la larghezza di banda è stata usata. Le righe di questa vista hanno base oraria. Ad esempio, 2009-09-19 02:00:00.000 indica che la larghezza di banda è stata usata il 19 settembre 2009 tra le 14.00 e le 3.00.|  
|**database_name**|Nome del database che ha usato la larghezza di banda.|  
|**direction**|Tipo di larghezza di banda usata, uno di:<br /><br /> Traffico in ingresso: Dati spostati nella [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Traffico in uscita: Dati spostati fuori il [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**class**|Classe di larghezza di banda usata, una di:<br />Interno: Dati spostati all'interno della piattaforma Azure.<br />Esterno: Dati spostati all'esterno della piattaforma Azure.<br /><br /> Questa classe viene restituita solo se il database è occupato in una relazione di copia continua tra aree ([!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]). Se un determinato database non fa parte di qualsiasi relazione di copia continua, le righe di "Interlink" non vengono restituite. Per ulteriori informazioni, vedere la sezione "Osservazioni" di seguito in questo argomento.|  
|**time_period**|Il periodo di tempo quando si è verificato durante l'utilizzo è picco o OffPeak. L'ora Peak si basa sull'area geografica in cui è stato creato il server. Ad esempio, se un server è stato creato nell'area geografica "US_Northwest", l'ora Peak è compresa tra le 10.00 e le 18.00 PST.|  
|**quantity**|La quantità di larghezza di banda, in kilobyte (KB), usata.|  
  
## <a name="permissions"></a>Permissions

 In questa vista è disponibile solo nel **master** database all'account di accesso dell'entità a livello di server.  
  
## <a name="remarks"></a>Note  
  
### <a name="external-and-internal-classes"></a>Classi External e Internal

 Per ogni database utilizzato in un determinato momento, il **Sys. bandwidth_usage** vista restituisce le righe che mostrano la classe e la direzione dell'utilizzo della larghezza di banda. Nell'esempio seguente vengono illustrati i dati che possono essere esposti per un determinato database. In questo esempio, la data e l'ora sono 2012-04-21 17:00:00, che cade nel periodo di massima attività. Il nome del database è Db1. In questo esempio **Sys. bandwidth_usage** ha restituito una riga per tutte e quattro le combinazioni di direzioni Ingress e in uscita e classi External e Internal, come indicato di seguito:  
  
|time|database_name|direction|classe|time_period|quantity|  
|----------|--------------------|---------------|-----------|------------------|--------------|  
|2012-04-21 17:00:00|Db1|Ingress|External|Peak|66|  
|2012-04-21 17:00:00|Db1|Egress|Altre informazioni|Peak|741|  
|2012-04-21 17:00:00|Db1|Ingress|Internal|Peak|1052|  
|2012-04-21 17:00:00|Db1|Egress|Interno|Peak|3525|  
  
### <a name="interpreting-data-direction-for-includessgeodrincludesssgeodr-mdmd"></a>Interpretazione della direzione dati per [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]

 Per la [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)], i dati di utilizzo della larghezza di banda sono visibili nel database master logico da entrambi i lati di una relazione di copia continua. Pertanto, è necessario interpretare il traffico in ingresso e in uscita indicatori di direzione dalla prospettiva del database che si esegue la query. Ad esempio, considerare un flusso di replica che trasferisce 1 MB di dati dal server di origine al server di destinazione. In questo caso, nel server di origine, il MB viene conteggiato nel totale dei dati inviati mentre nel server di destinazione, il MB viene registrato come dati ricevuti.  
  
> [!NOTE]  
> Il bulk dei dati vengono trasferiti dal server di origine al server di destinazione, nella direzione del flusso dei dati utente. Tuttavia, parte del trasferimento dei dati viene richiesto nell'altra direzione.  
