---
title: MSSQLSERVER_617 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 617 (Database Engine error)
ms.assetid: 213545d9-08a7-4427-bfd1-8b7e16644281
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dedf0b9ae26e7c2c1bb2c3251a1df10a3577f96d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053778"
---
# <a name="mssqlserver_617"></a>MSSQLSERVER_617
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|617|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|NODESHASH|  
|Testo del messaggio|Impossibile trovare nella tabella hash il descrittore per l'ID di oggetto %ld nel database con ID %d durante il tentativo di annullare l'hashing. Voce mancante in una tabella di lavoro. Eseguire nuovamente la query. Se viene utilizzato un cursore, chiuderlo e riaprirlo.|  
  
## <a name="explanation"></a>Spiegazione  
 SQL Server non è in grado di trovare la tabella di lavoro per una voce specifica.  
  
## <a name="user-action"></a>Azione dell'utente  
  
1.  Se viene utilizzato un cursore, chiuderlo e riaprirlo.  
  
2.  Eseguire nuovamente la query.  
  
  
