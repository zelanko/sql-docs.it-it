---
title: MSSQLSERVER_8712 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 465f47fd69f8e6477ede13892a079f069042c57b
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553036"
---
# <a name="mssqlserver_8712"></a>MSSQLSERVER_8712
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|8712|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|USEPLAN_ERR_NO_INDEX|  
|Testo del messaggio|L'indice '%.*ls' specificato nell'hint USE PLAN non esiste. Specificare un indice esistente o creare un indice con il nome specificato.|  
  
## <a name="explanation"></a>Spiegazione  
 Un indice specificato nell'hint USE PLAN non esiste.  
  
## <a name="user-action"></a>Azione dell'utente  
 Verificare che tutti gli indici specificati nell'hint USE PLAN esistano.  
  
## <a name="see-also"></a>Vedere anche  
 [Hint di query &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [Guide di piano](../performance/plan-guides.md)  
  
  
