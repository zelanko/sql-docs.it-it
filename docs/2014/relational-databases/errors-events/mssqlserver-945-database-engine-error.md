---
title: MSSQLSERVER_945 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 945 (Database Engine error)
ms.assetid: ee501d13-0bd9-4627-896c-ed5b1bdb88b3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f8c2cf1abfb41f4a49fccfe1befad11e429037da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62761741"
---
# <a name="mssqlserver945"></a>MSSQLSERVER_945
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|945|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DB_IS_SHUTDOWN|  
|Testo del messaggio|Impossibile aprire il database '%.*ls' a causa di file inaccessibili oppure per memoria o spazio su disco insufficiente.  Per ulteriori informazioni, vedere il log degli errori di SQL Server.|  
  
## <a name="explanation"></a>Spiegazione  
 Non è stato possibile accedere al database perché i file o altre risorse risultano mancanti.  
  
## <a name="user-action"></a>Azione dell'utente  
 Verificare se nel log degli errori sono presenti ulteriori informazioni sull'errore relativo alla memoria, allo spazio su disco o alle autorizzazioni. Verificare il percorso dei file con estensione mdf e ndf del database interessato. Verificare inoltre che l'account utilizzato dal [!INCLUDE[ssDE](../../includes/ssde-md.md)] disponga dell'autorizzazione per accedere a tali file. Dopo aver corretto il problema, riavviare il database utilizzando ALTER DATABASE per impostarlo su ONLINE.  
  
  
