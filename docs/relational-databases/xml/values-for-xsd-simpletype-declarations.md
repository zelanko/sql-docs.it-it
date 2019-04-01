---
title: Valori per dichiarazioni &lt;<xsd:simpleType>&gt; | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xsd:simpleType declarations
ms.assetid: 557b972d-3af9-40bf-8382-72b05c9de1c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a649b3e69286859c0293211b9f0ee3138daf5216
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510848"
---
# <a name="values-for-ltxsdsimpletypegt-declarations"></a>Valori per dichiarazioni &lt;<xsd:simpleType>&gt;
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Nella tabella seguente vengono descritte le restrizioni applicate, basate su tutte le enumerazioni di tipi semplici XSD riconosciute.  
  
 Inoltre, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta l'uso del valore NaN nelle dichiarazioni **\<xsd:simpleType>**. Gli schemi che includono valori NaN verranno rifiutati dal server.  
  
|Tipo semplice|Limitazione|  
|-----------------|----------------|  
|**duration**|La parte dell'anno deve essere all'interno dell'intervallo di -2^31 a 2^31-1. Il mese, il giorno, l'ora, il minuto e il secondo devono essere tutti all'interno dell'intervallo di 0 a 9999. La parte relativa ai secondi ha tre cifre aggiuntive di precisione a destra del separatore decimale.|  
|**dateTime**|La parte relativa all'ora nel sottocampo del fuso orario deve essere compresa nell'intervallo accettato di -14 a +14. La parte dell'anno deve essere compresa nell'intervallo da 1 a 9999. La parte del mese deve essere compresa nell'intervallo da 1 a 12. La parte del giorno deve essere compresa nell'intervallo da 1 a 31 e deve essere una data di calendario valida. Ad esempio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rileverà e restituirà un errore per una data non valida, nel caso di 31-02-1974, in quanto il mese di febbraio non include 31 giorni.<br /><br /> Il secondo componente supporta una precisione di 100 nanosecondi. L'indicazione del fuso orario è facoltativa.<br /><br /> SQL Server 2005 supporta anni nell'intervallo -9999 a 9999. Nella nuova versione di SQL Server è supportato un intervallo di anni minore. Per altre informazioni, vedere [Confrontare dati XML tipizzati con dati XML non tipizzati](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).|  
|**data**|La parte dell'anno deve essere compresa nell'intervallo da 1 a 9999. La parte del mese deve essere compresa nell'intervallo da 1 a 12. La parte del giorno deve essere compresa nell'intervallo da 1 a 31 e deve essere una data di calendario valida. Ad esempio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rileverà e restituirà un errore per una data non valida, nel caso di 31-02-1974, in quanto il mese di febbraio non include 31 giorni.<br /><br /> SQL Server 2005 supporta anni nell'intervallo -9999 a 9999. Nella nuova versione di SQL Server è supportato un intervallo di anni minore. Per altre informazioni, vedere [Confrontare dati XML tipizzati con dati XML non tipizzati](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).|  
|**gYearMonth**|La parte dell'anno deve essere compresa nell'intervallo da -9999 a 9999.|  
|**gYear**|La parte dell'anno deve essere compresa nell'intervallo da -9999 a 9999.|  
|**gMonthDay**|La parte del mese deve essere compresa nell'intervallo da 1 a 12. La parte del giorno deve essere compresa nell'intervallo da 1 a 31.|  
|**gDay**|La parte del giorno deve essere compresa nell'intervallo da 1 a 31|  
|**gMonth**|La parte del mese deve essere compresa nell'intervallo da 1 a 12.|  
|**decimal**|I valori di questo tipo devono essere conformi al formato di tipo numeric SQL. Questo rappresenta internamente il supporto per i numeri costituiti da un massimo di 38 cifre complessive, di cui 10 posizioni sono riservate alla precisione frazionaria.|  
|**float**|I valori di questo tipo devono essere conformi al formato del tipo SQL **reale** .|  
|**double**|I valori di questo tipo devono essere conformi al formato del tipo SQL **float** .|  
|**string**|I valori di questo tipo devono essere conformi al formato del tipo SQL **nvarchar(max)** .|  
|**anyURI**|La lunghezza dei valori di questo tipo non deve superare i 4000 caratteri Unicode.|  
  
## <a name="see-also"></a>Vedere anche  
 [Requisiti e limitazioni per l'utilizzo di raccolte di XML Schema nel server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
