---
title: sp_configure_peerconflictdetection (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_configure_peerconflictdetection_TSQL
- sp_configure_peerconflictdetection
helpviewer_keywords:
- sp_configure_peerconflictdetection
ms.assetid: 45117cb2-3247-433f-ba3d-7fa19514b1c3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8a8cc9930ddf85dea60999e3b63dbcebaaf42d8f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68215948"
---
# <a name="sp_configure_peerconflictdetection-transact-sql"></a>sp_configure_peerconflictdetection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Configura il rilevamento dei conflitti per una pubblicazione coinvolta in una topologia di replica transazionale peer-to-peer. Per altre informazioni, vedere [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md). Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_configure_peerconflictdetection [ @publication = ] 'publication'  
    [ , [ @action = ] 'action']  
    [ , [ @originator_id = ] originator_id ]  
    [ , [ @conflict_retention = ] conflict_retention ]  
    [ , [ @continue_onconflict = ] 'continue_onconflict']  
    [ , [ @local = ] 'local']  
    [ , [ @timeout = ] timeout ]  
  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @publication=] '*Publication*'  
 Nome della pubblicazione per cui si desidera configurare il rilevamento dei conflitti. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
 [ @action= ] '*azione*'  
 Specifica se abilitare o disabilitare il rilevamento dei conflitti per una pubblicazione. *Action* è di **tipo nvarchar (5)**. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Abilita**|Abilita il rilevamento dei conflitti per una pubblicazione.|  
|**disabilitare**|Disabilita il rilevamento dei conflitti per una pubblicazione.|  
|NULL (predefinito)||  
  
 [ @originator_id= ] *originator_id*  
 Specifica un ID per un nodo in una topologia peer-to-peer. *originator_id* è di **tipo int**e il valore predefinito è null. Questo ID viene utilizzato per il rilevamento dei conflitti se l' *azione* è impostata su **Abilita**. Specificare un ID positivo diverso da zero che non sia mai stato utilizzato nella topologia. Per un elenco degli ID che sono già stati utilizzati, eseguire una query sulla tabella di sistema [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) .  
  
 [ @conflict_retention= ] *conflict_retention*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @continue_onconflict= ] '*continue_onconflict*']  
 Determina se l'agente di distribuzione continua a elaborare le modifiche dopo che è stato rilevato un conflitto. *continue_onconflict* è di **tipo nvarchar (5)** e il valore predefinito è false.  
  
> [!CAUTION]  
>  È consigliabile utilizzare il valore predefinito FALSE. Quando questa opzione è impostata su TRUE, l'agente di distribuzione tenta di garantire la convergenza dei dati nella topologia applicando la riga in conflitto dal nodo con ID di origine maggiore. Questo metodo non garantisce la convergenza. Dopo il rilevamento di un conflitto, è necessario assicurarsi che la topologia sia coerente. Per ulteriori informazioni, vedere la sezione relativa alla gestione dei conflitti in [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
 [ @local= ] '*local*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @timeout= ] *timeout*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 sp_configure_peerconflictdetection è utilizzato nella replica transazionale peer-to-peer. Per usare il rilevamento dei conflitti, tutti i nodi [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] devono eseguire o versioni successive. e il rilevamento deve essere abilitato per tutti i nodi.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del server sysadmin o al ruolo predefinito del database db_owner.  
  
## <a name="see-also"></a>Vedere anche  
 [Peer-to-peer - Rilevamento dei conflitti nella replica](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)   
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
