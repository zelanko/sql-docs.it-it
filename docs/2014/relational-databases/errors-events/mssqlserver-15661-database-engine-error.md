---
title: MSSQLSERVER_15661 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 15661 (Database Engine error)
ms.assetid: 88b01bfb-74ce-4aa0-aec0-7885261c7ef3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 31e24d4cd5e790751b4a43773f2b7d0156b4b7da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915457"
---
# <a name="mssqlserver15661"></a>MSSQLSERVER_15661
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|15661|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SQLErrorNum15661|  
|Testo del messaggio|Impossibile utilizzare la stored procedure sp_estimate_data_compression_savings per le tabelle temporanee.|  
  
## <a name="explanation"></a>Spiegazione  
 Una tabella temporanea è stata usata come argomento per la stored procedure sp_estimate_data_compression_savings. Sebbene la compressione delle tabelle temporanee sia supportata, non è possibile usare sp_estimate_data_compression_savings per stimare il risparmio in caso di compressione.  
  
## <a name="user-action"></a>Azione dell'utente  
 Rimuovere la tabella temporanea come argomento per sp_estimate_data_compression_savings.  
  
  
