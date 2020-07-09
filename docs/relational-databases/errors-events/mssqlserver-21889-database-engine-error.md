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
ms.openlocfilehash: 6ff8af9c4abe6f2784f153f8d8346b2609d3197b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780514"
---
# <a name="mssqlserver_21889"></a>MSSQLSERVER_21889
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
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
  
