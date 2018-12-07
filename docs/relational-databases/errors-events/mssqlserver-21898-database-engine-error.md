---
title: MSSQLSERVER_21898 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21898 (Database Engine error)
ms.assetid: 02405b21-3d4e-4c2d-b4b3-d7b1ec05edb4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2d96408100616f6939c7a61ea7a76a69e8b4a1e7
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52398715"
---
# <a name="mssqlserver21898"></a>MSSQLSERVER_21898
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|21898|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SQLErrorNum21898|  
|Testo del messaggio|Il server di pubblicazione '%s' utilizza il database di distribuzione '%s' e non '%s' che è richiesto per ospitare il database di pubblicazione '%s.' Eseguire **sp_changedistpublisher** sul database di distribuzione '%s' per modificare il database di distribuzione usato dal server di pubblicazione in '%s'.|  
  
## <a name="explanation"></a>Spiegazione  
**sp_validate_redirected_publisher** esegue una query di msdb.dbo.MSdistpublishers nel database di distribuzione locale per verificare che il database di distribuzione usato dal nuovo server di pubblicazione sia uguale a quello usato dal server di pubblicazione originale. Questo errore viene restituito quando questi database sono diversi, rendendo il server di pubblicazione un host non adatto al database del server di pubblicazione.  
  
## <a name="user-action"></a>Azione dell'utente  
Eseguire la stored procedure **sp_changedistpublisher** per modificare il database di distribuzione per il nuovo server di pubblicazione usato dal server di pubblicazione originale.  
  
> [!NOTE]  
> Con l'esecuzione di **sp_changedistpublisher** il problema verrà indirizzato se è stato immesso il database di distribuzione errato durante l'esecuzione di **sp_adddistpublisher** sul database di distribuzione per il server di pubblicazione. Tuttavia, se il server di pubblicazione remoto dispone di pubblicazioni esistenti di un altro database di pubblicazione che utilizza il database di distribuzione identificato, questa modifica non è adatta. La replica con il database di distribuzione denominato deve essere rimossa sistematicamente e quindi ristabilita usando il database di distribuzione del server di pubblicazione originale affinché il nuovo server di pubblicazione funzioni come un host adatto.  
  
