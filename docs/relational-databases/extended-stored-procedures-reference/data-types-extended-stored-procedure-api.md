---
title: Tipi di dati (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], data types
- data types [SQL Server], extended stored procedures
ms.assetid: 37fb86b9-8819-4387-bcdc-9616968e15ad
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1aed9ac46d81e57a47f1026e599a5e50818190a8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62742189"
---
# <a name="data-types-extended-stored-procedure-api"></a>Tipi di dati (API Stored procedure estesa)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Per utilizzare i tipi di dati dell'API Stored procedure estesa, includere il file di intestazione Srv.h nel programma.  
  
|Tipo di dati|Tipo di dati di SQL Server|Descrizione|  
|---------------|--------------------------|-----------------|  
|SRVBIGBINARY|**binary**|Tipo di dati **binary**, lunghezza compresa tra 0 e 8000 byte.|  
|SRVBIGCHAR|**char**|Tipo di dati **character**, lunghezza compresa tra 0 e 8000 byte.|  
|SRVBIGVARBINARY|**varbinary**|Tipo di dati **binary** a lunghezza variabile compresa tra 0 e 8000 byte.|  
|SRVBIGVARCHAR|**varchar**|Tipo di dati **character** a lunghezza variabile compresa tra 0 e 8000 byte.|  
|SRVBINARY|**binary**|Tipo di dati **binary**.|  
|SRVBIT|**Bit**|Tipo di dati **bit**.|  
|SRVBITN|**bit null**|Tipo di dati **bit**, sono consentiti valori Null.|  
|SRVCHAR|**char**|Tipo di dati **character**.|  
|SRVDATETIME|**datetime**|Tipo di dati **datetime** a 8 byte.|  
|SRVDATETIM4|**smalldatetime**|Tipo di dati **smalldatetime** a 4 byte.|  
|SRVDATETIMN|**datetime null**|Tipo di dati **smalldatetime** o **datetime**, sono consentiti valori Null.|  
|SRVDECIMAL|**decimal**|Tipo di dati **decimal**.|  
|SRVDECIMALN|**decimal null**|Tipo di dati **decimal**, sono consentiti valori Null.|  
|SRVFLT4|**real**|Tipo di dati **real** a 4 byte.|  
|SRVFLT8|**float**|Tipo di dati **float** a 8 byte.|  
|SRVFLTN|**real** &#124; **float null**|Tipo di dati **real** o **float**, sono consentiti valori Null.|  
|SRVIMAGE|**image**|Tipo di dati **image**.|  
|SRVINT1|**tinyint**|Tipo di dati **tinyint** a 1 byte.|  
|SRVINT2|**smallint**|Tipo di dati **smallint** a 2 byte.|  
|SRVINT4|**int**|Tipo di dati **int** a 4 byte.|  
|SRVINTN|**tinyint** &#124; **smallint** &#124; **int null**|Tipo di dati **tinyint**, **smallint** o **int**, sono consentiti valori Null.|  
|SRVMONEY4|**smallmoney**|Tipo di dati **smallmoney** a 4 byte.|  
|SRVMONEY|**money**|Tipo di dati **money** a 8 byte.|  
|SRVMONEYN|**money** &#124; **smallmoney null**|Tipo di dati **smallmoney** o **money**, sono consentiti valori Null.|  
|SRVNCHAR|**nchar**|Tipo di dati **character** Unicode.|  
|SRVNTEXT|**ntext**|Tipo di dati **text** Unicode.|  
|SRVNUMERIC|**numeric**|Tipo di dati **numeric**.|  
|SRVNUMERICN|**numeric null**|Tipo di dati **numeric**, sono consentiti valori Null.|  
|SRVNVARCHAR|**nvarchar**|Tipo di dati **character** a lunghezza variabile Unicode.|  
|SRVTEXT|**text**|Tipo di dati **text**.|  
|SRVVARBINARY|**varbinary**|Tipo di dati **binary** a lunghezza variabile.|  
|SRVVARCHAR|**varchar**|Tipo di dati **character** a lunghezza variabile.|  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
