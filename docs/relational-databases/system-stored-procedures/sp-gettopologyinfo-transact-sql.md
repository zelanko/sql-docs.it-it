---
title: sp_gettopologyinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_gettopologyinfo_TSQL
- sp_gettopologyinfo
helpviewer_keywords:
- sp_gettopologyinfo
ms.assetid: 8bbe8a06-a4aa-4219-8402-12db6a4682c6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4b5532a5c9dfba03a0e2b9b2fe649912cd0535cc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52764553"
---
# <a name="spgettopologyinfo-transact-sql"></a>sp_gettopologyinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sulla topologia di replica transazionale peer-to-peer. Eseguire [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) per raccogliere informazioni prima di eseguire questa procedura.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_gettopologyinfo [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @request_id=] *request_id*  
 ID di una richiesta di stato di topologia. *request_id* viene **int**, con un valore predefinito è NULL. Per ottenere un ID, utilizzare il @request_id dal parametro di output [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) oppure eseguire una query il [MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md) tabella di sistema.  
  
## <a name="result-sets"></a>Set di risultati  
 sp_gettopologyinfo restituisce un set di risultati con un'unica colonna XML. I dati nella colonna XML sono quello utilizzato per i dati di [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) tabella di sistema.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 sp_gettopologyinfo viene utilizzato nella replica transazionale peer-to-peer. Eseguire [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) prima di eseguire sp_gettopologyinfo. Queste procedure vengono utilizzate dalla Configurazione guidata topologia peer-to-peer, ma possono anche essere utilizzate direttamente se si richiedono informazioni sulla topologia in un formato XML. Se si preferiscono risultati tabulari, eseguire una query di [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) tabella di sistema.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo predefinito del server sysadmin o al ruolo predefinito del database db_owner.  
  
## <a name="see-also"></a>Vedere anche  
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
