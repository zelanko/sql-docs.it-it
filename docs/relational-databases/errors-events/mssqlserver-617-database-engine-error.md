---
title: MSSQLSERVER_617 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 617 (Database Engine error)
ms.assetid: 213545d9-08a7-4427-bfd1-8b7e16644281
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f5078c98445587dbf8c8b99fa18fed4df2ca5846
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "67951660"
---
# <a name="mssqlserver_617"></a>MSSQLSERVER_617
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
