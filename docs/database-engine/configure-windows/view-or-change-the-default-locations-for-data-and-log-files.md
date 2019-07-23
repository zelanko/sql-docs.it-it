---
title: Visualizzare o modificare i percorsi predefiniti per i file di dati e di log | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- log files [SQL Server], changing default location
- data files [SQL Server], changing default location
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 933d15e789e0d069822f657ff09cff0e2b4aaf8c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945750"
---
# <a name="view-or-change-the-default-locations-for-data-and-log-files"></a>Visualizzare o modificare i percorsi predefiniti per i file di dati e di log
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
 La procedura consigliata per la protezione dei file di dati e di log consiste nel verificare che siano protetti da elenchi di controllo di accesso (ACL). Impostare gli elenchi di controllo di accesso a livello della radice in cui vengono creati i file.  
 
  
## <a name="view-or-change-the-default-locations-for-database-files"></a>Visualizzare o modificare i percorsi predefiniti per i file di database  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse sul server e scegliere **Proprietà**.  
  
2.  Nel riquadro sinistro della pagina Proprietà fare clic sulla scheda **Impostazioni database** .  
  
3.  Nel pannello **Percorsi predefiniti database**è possibile visualizzare i percorsi predefiniti correnti per i nuovi file di dati e di log. Per modificare un percorso predefinito, immettere un nuovo percorso predefinito nel campo **Dati** o **Log** oppure fare clic sul pulsante Sfoglia per individuare e selezionare un percorso.  
  
>**NOTA** dopo aver modificato i percorsi predefiniti, è necessario arrestare e avviare il servizio SQL Server per completare la modifica.  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Creare un database](../../relational-databases/databases/create-a-database.md)  
  
  
