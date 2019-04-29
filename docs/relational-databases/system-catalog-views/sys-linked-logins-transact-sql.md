---
title: sys.linked_logins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.linked_logins
- sys.linked_logins_TSQL
- linked_logins_TSQL
- linked_logins
dev_langs:
- TSQL
helpviewer_keywords:
- sys.linked_logins catalog view
ms.assetid: af57bf0c-a265-410f-9bab-63b78569b4a6
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 712d5286036aa8fbf375d16abfbe3a3c2257ab91
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004269"
---
# <a name="syslinkedlogins-transact-sql"></a>sys.linked_logins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni mapping dell'account di accesso al server collegato, per l'utilizzo in RPC e query distribuite dal server locale al server collegato corrispondente.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|ID del server nella **Sys. Servers**.|  
|**local_principal_id**|**int**|Entità server a cui viene applicato il mapping.<br /><br /> 0 = carattere jolly o pubblico.|  
|**uses_self_credential**|**bit**|Se è 1, il mapping indica che devono essere utilizzate credenziali specifiche della sessione. Se è 0, significa che nella sessione vengono utilizzati il nome e la password specificati.|  
|**remote_name**|**sysname**|Nome utente remoto da utilizzare per la connessione. La password viene archiviata, ma non è esposta nelle interfacce delle viste del catalogo.|  
|**modify_date**|**datetime**|Data dell'ultima modifica dell'account di accesso collegato.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Viste del catalogo di server collegati &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)  
  
  
