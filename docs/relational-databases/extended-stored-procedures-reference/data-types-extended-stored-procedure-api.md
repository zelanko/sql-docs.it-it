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
ms.openlocfilehash: 1e135e6706454fe1f03b4c7ab762e5234e1b7d35
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064212"
---
# <a name="data-types-extended-stored-procedure-api"></a>Tipi di dati (API Stored procedure estesa)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  
  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Per utilizzare i tipi di dati dell'API Stored procedure estesa, includere il file di intestazione Srv.h nel programma.  
  
|Tipo di dati|Tipo di dati di SQL Server|Descrizione|  
|---------------|--------------------------|-----------------|  
|SRVBIGBINARY|**BINARY**|tipo di dati **Binary** , da 0 a 8000 byte.|  
|SRVBIGCHAR|**char**|tipo di dati **character** , da 0 a 8000 byte.|  
|SRVBIGVARBINARY|**varbinary**|Tipo di dati **binary** a lunghezza variabile compresa tra 0 e 8000 byte.|  
|SRVBIGVARCHAR|**varchar**|Tipo di dati **character** a lunghezza variabile compresa tra 0 e 8000 byte.|  
|SRVBINARY|**BINARY**|tipo di dati **Binary** .|  
|SRVBIT|**Po'**|tipo di dati **bit** .|  
|SRVBITN|**bit null**|tipo di dati **bit** , sono consentiti valori null.|  
|SRVCHAR|**char**|tipo di dati **character** .|  
|SRVDATETIME|**datetime**|Tipo di dati **datetime** a 8 byte.|  
|SRVDATETIM4|**smalldatetime**|Tipo di dati **smalldatetime** a 4 byte.|  
|SRVDATETIMN|**DateTime null**|tipo di dati **smalldatetime** o **DateTime** , sono consentiti valori null.|  
|SRVDECIMAL|**decimal**|tipo di dati **Decimal** .|  
|SRVDECIMALN|**null decimale**|tipo di dati **Decimal** , sono consentiti valori null.|  
|SRVFLT4|**reale**|Tipo di dati **real** a 4 byte.|  
|SRVFLT8|**float**|Tipo di dati **float** a 8 byte.|  
|SRVFLTN|**real** &#124; **float null**|tipo di dati **Real** o **float** , sono consentiti valori null.|  
|SRVIMAGE|**immagine**|tipo di dati **Image** .|  
|SRVINT1|**tinyint**|Tipo di dati **tinyint** a 1 byte.|  
|SRVINT2|**smallint**|Tipo di dati **smallint** a 2 byte.|  
|SRVINT4|**int**|Tipo di dati **int** a 4 byte.|  
|SRVINTN|**tinyint** &#124; **smallint** &#124; **int null**|tipo di dati **tinyint**, **smallint**o **int** , sono consentiti valori null.|  
|SRVMONEY4|**SMALLMONEY**|Tipo di dati **smallmoney** a 4 byte.|  
|SRVMONEY|**money**|Tipo di dati **money** a 8 byte.|  
|SRVMONEYN|**money** &#124; **smallmoney null**|tipo di dati **smallmoney** o **Money** , sono consentiti valori null.|  
|SRVNCHAR|**nchar**|Tipo di dati **character** Unicode.|  
|SRVNTEXT|**ntext**|Tipo di dati **text** Unicode.|  
|SRVNUMERIC|**numerico**|tipo di dati **numeric** .|  
|SRVNUMERICN|**valore null numerico**|tipo di dati **numeric** , sono consentiti valori null.|  
|SRVNVARCHAR|**nvarchar**|Tipo di dati **character** a lunghezza variabile Unicode.|  
|SRVTEXT|**text**|tipo di dati **Text** .|  
|SRVVARBINARY|**varbinary**|Tipo di dati **binary** a lunghezza variabile.|  
|SRVVARCHAR|**varchar**|Tipo di dati **character** a lunghezza variabile.|  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
