---
title: MSSQLSERVER_1461 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1461 (Database Engine error)
ms.assetid: fce10907-4753-441b-b624-f28e00ed7520
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0af23b53c60ffeafcbaa99a7a499fe0a71cd551b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62869828"
---
# <a name="mssqlserver_1461"></a>MSSQLSERVER_1461
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|1461|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBM_SAFETY_MISMATCH|  
|Testo del messaggio|Rilevati livelli di protezione del mirroring del database diversi tra i server per il database "%.*ls". Verrà utilizzato il livello di protezione FULL.|  
  
## <a name="explanation"></a>Spiegazione  
 Le connessioni per il mirroring sono state interrotte quando il livello di protezione delle transazioni è stato modificato a causa dell'inconsistenza delle impostazioni di protezione delle transazioni nei database principale e mirror. Verrà utilizzata l'impostazione predefinita del livello di protezione FULL delle transazioni. La sessione verrà eseguita in modalità a protezione elevata.  
  
## <a name="user-action"></a>Azione dell'utente  
 Per disattivare la protezione delle transazioni, eseguire nuovamente l'istruzione ALTER DATABASE *nome_database* SET PARTNER SAFETY OFF nel database principale.  
  
  
