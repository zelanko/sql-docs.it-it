---
title: MSSQLSERVER_21889 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21889 (Database Engine error)
ms.assetid: ae199540-7986-4cc2-b782-cd22793236d3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 177da1486d7cab622bacaea56cd886bd8dc06d06
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "72251495"
---
# <a name="mssqlserver_21889"></a>MSSQLSERVER_21889
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|21889|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SQLErrorNum21889|  
|Testo del messaggio|L'istanza di SQL Server '%s' non è un server di pubblicazione della replica. Eseguire **sp_adddistributor** sull'istanza di SQL Server '%s' con il database di distribuzione '%s' per consentire all'istanza di ospitare il database di pubblicazione '%s'. Assicurarsi di specificare lo stesso account di accesso e password di quello utilizzato per il server di pubblicazione originale.|  
  
## <a name="explanation"></a>Spiegazione  
Per ospitare il database del server di pubblicazione, l'istanza di SQL Server deve essere un server di pubblicazione di replica. **sp_validate_redirected_publisher** chiama **sp_helpdistributor** sul server remoto per determinare se il server è un server di pubblicazione di replica. Questo errore indica che l'istanza di destinazione di SQL Server non è un server di pubblicazione di replica.  
  
## <a name="user-action"></a>Azione dell'utente  
Eseguire **sp_adddistributor** sull'istanza di SQL Server che ospita il database del server di pubblicazione. Quando si esegue **sp_adddistributor**, specificare il database di distribuzione corretto. Per il parametro *\@password* usare lo stesso valore usato quando **sp_adddistributor** è stato inizialmente eseguito nel database di distribuzione.  
  
