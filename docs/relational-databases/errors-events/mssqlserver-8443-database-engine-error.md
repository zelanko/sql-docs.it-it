---
description: MSSQLSERVER_8443
title: MSSQLSERVER_8443 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8443 (Database Engine error)
ms.assetid: a3541b9c-b1a8-4280-add1-275f08696b62
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2369961f0fc805bf51b4fe9fd5372d6ebbf065d7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420995"
---
# <a name="mssqlserver_8443"></a>MSSQLSERVER_8443
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|8443|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SB_DIALOG_WO_CONV_GROUP|  
|Testo del messaggio|La conversazione con ID '%.*ls' e Initiator %d fa riferimento al gruppo di conversazione mancante '%.\*ls'. Eseguire DBCC CHECKDB per analizzare e riparare il database.|  
  
## <a name="explanation"></a>Spiegazione  
Il livello di metadati ha restituito NULL per il gruppo di conversazione. Il database è stato danneggiato in qualche modo. Una possibile causa di danneggiamento è un errore del disco.  
  
## <a name="user-action"></a>Azione dell'utente  
Eseguire DBCC CHECKDB in modalità di correzione per riportare il database in uno stato consistente. I messaggi potrebbero essere eliminati se necessario per ripristinare la consistenza. Verificare i log degli errori di sistema per vedere se l'errore è stato causato da un altro malfunzionamento del sistema.  
  
