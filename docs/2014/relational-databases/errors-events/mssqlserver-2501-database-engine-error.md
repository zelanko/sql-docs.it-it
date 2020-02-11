---
title: MSSQLSERVER_2501 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2501 (Database Engine error)
ms.assetid: 895aafe3-a4e7-4ed8-acc5-93be76ef3664
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9d4920be6af560cbd5bd1d7699dd6378cdc2db3b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62914851"
---
# <a name="mssqlserver_2501"></a>MSSQLSERVER_2501
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|2501|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC_NO_SUCH_TABLE_NAME|  
|Testo del messaggio|Impossibile trovare un oggetto o una tabella con il nome 'NAME'. Controllare il catalogo di sistema.|  
  
## <a name="explanation"></a>Spiegazione  
 Non è possibile individuare l'oggetto specificato.  
  
### <a name="possible-causes"></a>Possibili cause  
 L'errore può essere causato da uno dei problemi seguenti:  
  
-   L'oggetto non è stato specificato correttamente.  
  
-   L'oggetto non esiste o è stato rimosso prima di essere utilizzato in un'istruzione.  
  
-   È possibile che l'oggetto esista ma non possa essere esposto all'utente. Ad esempio, l'utente potrebbe non disporre di autorizzazioni sufficienti per visualizzare l'oggetto oppure l'oggetto è costituito da una tabella interna che non può essere visualizzata dall'utente.  
  
## <a name="user-action"></a>Azione dell'utente  
  
-   Verificare la correttezza del contesto di database corrente. Per altre informazioni, vedere [USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql).  
  
-   Verificare che il nome della tabella o dell'oggetto sia stato specificato correttamente.  
  
-   Verificare il nome dello schema contenente l'oggetto. Se l'oggetto appartiene a uno schema diverso da quello predefinito, ovvero **dbo**, è necessario specificare il nome della tabella o dell'oggetto usando il formato in due parti *schema_name.object_name*.  
  
-   Verificare l'esistenza dell'oggetto nelle tabelle di sistema. Per verificare l'esistenza di una tabella o un altro oggetto con ambito schema, eseguire una query nella vista del catalogo [sys.objects](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql). Se l'oggetto non è presente nelle tabelle di sistema, significa che è stato eliminato o l'utente non dispone delle autorizzazioni necessarie per visualizzare i metadati dell'oggetto. Per altre informazioni su come visualizzare i metadati degli oggetti, vedere [Configurazione della visibilità dei metadati](../security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql)  
  
  
