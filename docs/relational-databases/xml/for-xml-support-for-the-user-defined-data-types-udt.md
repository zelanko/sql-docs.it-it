---
title: Supporto di FOR XML per i tipi di dati definiti dall'utente (UDT) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- UDTs [SQL Server], XML
- user-defined types [SQL Server], XML
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2416bdc2b49a88b4306ae46973eab70fc38c0d9d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943252"
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>Supporto di FOR XML per i tipi di dati definiti dall'utente (UDT)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  FOR XML non supporta tipi di dati definiti dall'utente Common Language Runtime (CLR).  
  
 Per utilizzare FOR XML con tipi di dati definiti dall'utente CLR, assicurarsi che il tipo di dati abbia una serializzazione XML e utilizzare un cast esplicito per XML nella clausola scelta FOR XML.  
  
## <a name="see-also"></a>Vedere anche  
 [Supporto di FOR XML per vari tipi di dati di SQL Server](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
