---
title: MSSQLSERVER_15404 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 15404 (Database Engine error)
ms.assetid: 69677f02-bc81-4e4a-99b8-5c1bd1de36df
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1bf1e56219b7d26e326b69d9a2f2d88afdd8c4a9
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553776"
---
# <a name="mssqlserver_15404"></a>MSSQLSERVER_15404
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|15404|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SEC_NTGRP_ERROR|  
|Testo del messaggio|Non è stato possibile ottenere informazioni relative al gruppo/utente di Windows NT '*user*', codice di errore *code*.|  
  
## <a name="explanation"></a>Spiegazione  
 L'errore 15404 è utilizzato nell'autenticazione quando si specifica un'entità non valida. In alternativa, la rappresentazione di un account di Windows ha esito negativo poiché non esiste alcuna relazione di trust completo tra l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il dominio dell'account di Windows.  
  
## <a name="user-action"></a>Azione dell'utente  
 Verificare che l'entità di Windows esista e non siano stati commessi errori di digitazione.  
  
 Se questo errore è dovuto all'assenza di una relazione di trust completo tra l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il dominio dell'account di Windows, è possibile risolvere il problema tramite una delle azioni seguenti:  
  
-   Utilizzare un account dello stesso dominio dell'utente di Windows per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza un account computer, ad esempio Servizio di rete o Sistema locale, il computer deve essere considerato attendibile dal dominio che contiene l'utente di Windows.  
  
-   Utilizzare un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
