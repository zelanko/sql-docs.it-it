---
title: MSSQLSERVER_360 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 360 (Database Engine error)
ms.assetid: e2b7c1b2-3679-4206-9b25-6bd55ef96a2c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b30311d7f55231c1e7a6d5969d49c5d1bc07a848
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033379"
---
# <a name="mssqlserver_360"></a>MSSQLSERVER_360
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|360|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DML_UPDATE_SPARSE_AND_COLSET|  
|Testo del messaggio|L'elenco delle colonne di destinazione di un'istruzione INSERT, UPDATE o MERGE non può includere sia una colonna di tipo sparse sia il set di colonne che contiene tale colonna. Riscrivere l'istruzione in modo che includa la colonna di tipo sparse o il set di colonne, ma non entrambi.|  
  
## <a name="explanation"></a>Spiegazione  
 Un set di colonne è una rappresentazione XML non tipizzata che combina alcune colonne di una tabella in un output strutturato. È stato effettuato un tentativo di modificare sia il set di colonne che una colonna inclusa nel set, provocando due riferimenti alla stessa colonna.  
  
## <a name="user-action"></a>Azione dell'utente  
 Riscrivere l'istruzione in modo che includa i riferimenti o alla colonna oppure al set di colonne, ma non a entrambi.  
  
  
