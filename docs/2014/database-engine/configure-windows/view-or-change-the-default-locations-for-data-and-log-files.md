---
title: Visualizzare o modificare i percorsi predefiniti per i file di dati e di log (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- log files [SQL Server], changing default location
- data files [SQL Server], changing default location
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 06d17a4feaec0db614f61fb7761b37ea415efc24
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62808711"
---
# <a name="view-or-change-the-default-locations-for-data-and-log-files-sql-server-management-studio"></a>Visualizzazione o modifica dei percorsi predefiniti per i file di dati e di log (SQL Server Management Studio)
  In questo argomento si descrive come visualizzare e modificare i percorsi predefiniti dei nuovi file di dati e di log in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Il percorso predefinito viene ottenuto dal Registro di sistema. Dopo la modifica, il percorso viene utilizzato in tutti i nuovi database creati nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se non è specificato un percorso diverso.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Indicazioni](#Recommendations)  
  
-   **Per visualizzare o modificare i percorsi predefiniti per i file di dati e di log utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
-   **Completamento:**  [modifica dei percorsi predefiniti](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Recommendations"></a> Raccomandazioni  
 La procedura consigliata per la protezione dei file di dati e di log consiste nel verificare che siano protetti da elenchi di controllo di accesso (ACL). Gli elenchi di controllo di accesso devono essere impostati a livello della radice in cui vengono creati i file.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-default-locations-for-database-files"></a>Per visualizzare o modificare i percorsi predefiniti per i file di database  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server, quindi scegliere **Proprietà**.  
  
2.  Nel pannello sinistro fare clic sulla pagina **Impostazioni database** .  
  
3.  Nel pannello **Percorsi predefiniti database**è possibile visualizzare i percorsi predefiniti correnti per i nuovi file di dati e di log. Per modificare un percorso predefinito, immettere un nuovo percorso predefinito nel campo **Dati** o **Log** oppure fare clic sul pulsante Sfoglia per individuare e selezionare un percorso.  
  
##  <a name="FollowUp"></a>Completamento: dopo la modifica dei percorsi predefiniti  
 È necessario arrestare e avviare il servizio SQL Server per completare la modifica.  
  
## <a name="see-also"></a>Vedere anche  
 [CREAZIONE di &#40;di DATABASE SQL Server&#41;Transact-SQL](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [Creare un database](../../relational-databases/databases/create-a-database.md)  
  
  
