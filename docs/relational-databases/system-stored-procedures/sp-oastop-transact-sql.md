---
description: sp_OAStop (Transact-SQL)
title: sp_OAStop (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAStop
- sp_OAStop_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAStop
ms.assetid: aa9eab66-c4f7-4ec7-9f0d-5d24d16da654
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1ec53c344fc3b69351c8b7e5d8165db1120471c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473943"
---
# <a name="sp_oastop-transact-sql"></a>sp_OAStop (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Arresta l'ambiente di esecuzione delle stored procedure di automazione OLE nell'intero server.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_OAStop      
```  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (esito positivo) o un numero diverso da zero (esito negativo) corrispondente al valore intero del codice HRESULT restituito dall'oggetto di automazione OLE.  
  
 Per ulteriori informazioni sui codici restituiti HRESULT, vedere [codici restituiti e informazioni sugli errori di automazione OLE](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="remarks"></a>Osservazioni  
 Tutti i client che utilizzano le stored procedure di automazione OLE condividono uno stesso ambiente di esecuzione. Se un client chiama **sp_OAStop** l'ambiente di esecuzione condiviso verrà interrotto per tutti i client. Dopo che l'ambiente di esecuzione è stato interrotto, qualsiasi chiamata a **sp_OACreate** riavvia l'ambiente di esecuzione.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** o l'autorizzazione Execute direttamente in questa stored procedure. `Ole Automation Procedures` la configurazione deve essere **abilitata** per l'utilizzo di qualsiasi procedura di sistema correlata all'automazione OLE.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene arrestato l'ambiente di esecuzione di automazione OLE condiviso.  
  
```  
EXEC sp_OAStop;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di automazione OLE &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Script di automazione OLE di esempio](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
