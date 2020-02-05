---
title: DROP AVAILABILITY GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_AVAILABILITY_GROUP_TSQL
- DROP AVAILABILITY GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], Transact-SQL statements
- DROP AVAILABILITY GROUP statement
- Availability Groups [SQL Server], dropping
ms.assetid: c1600289-c990-454a-b279-dba0ebd5d63e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 613841598b153dbe502f0267ed85197973bf706a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "67898302"
---
# <a name="drop-availability-group-transact-sql"></a>DROP AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Rimuove il gruppo di disponibilità specificato e tutte le relative repliche. Se un'istanza del server che ospita una delle repliche di disponibilità è offline quando si elimina un gruppo di disponibilità, la replica di disponibilità locale verrà eliminata dall'istanza del server quando torna online. La rimozione di un gruppo di disponibilità comporta l'eliminazione dell'eventuale listener del gruppo di disponibilità associato.  
  
> [!IMPORTANT]  
>  Se possibile, rimuovere il gruppo di disponibilità solo se connesso all'istanza del server in cui è ospitata la replica primaria. Se il gruppo di disponibilità viene rimosso dalla replica primaria, sono consentite modifiche nei database primari precedenti (senza protezione a disponibilità elevata). Eliminando un gruppo di disponibilità da una replica secondaria, la replica primaria viene mantenuta nello stato **RESTORING** e non sono consentite modifiche nei database.  
  
 Per informazioni sui metodi alternativi per eliminare un gruppo di disponibilità, vedere [Rimuovere un gruppo di disponibilità &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DROP AVAILABILITY GROUP group_name   
[ ; ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *group_name*  
 Specifica il nome del gruppo di disponibilità da eliminare.  
  
## <a name="limitations-and-recommendations"></a>Limitazioni e consigli  
  
-   L'esecuzione di **DROP AVAILABILITY GROUP** richiede che la funzionalità Gruppi di disponibilità AlwaysOn sia abilitata nell'istanza del server. Per altre informazioni, vedere [Abilitare e disabilitare la funzionalità Gruppi di disponibilità Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
-   Non è possibile eseguire **DROP AVAILABILITY GROUP** come parte di batch o all'interno di transazioni. Le espressioni e le variabili non sono supportate.  
  
-   È possibile eliminare un gruppo di disponibilità da qualsiasi nodo WSFC (Windows Server Failover Clustering) che disponga delle credenziali di sicurezza corrette per il gruppo di disponibilità. In questo modo, è possibile eliminare un gruppo di disponibilità quando non rimane nessuna delle relative repliche di disponibilità.  
  
    > [!IMPORTANT]  
    >  Evitare di eliminare un gruppo di disponibilità se il cluster WSFC (Windows Server Failover Clustering) non dispone di quorum. Se è necessario eliminare un gruppo di disponibilità quando il cluster non dispone di quorum, non verrà rimosso il gruppo di disponibilità dei metadati archiviato nel cluster. Una volta che il cluster avrà riacquisito il quorum, sarà necessario eliminare nuovamente il gruppo di disponibilità per rimuoverlo dal cluster WSFC.  
  
-   In una replica secondaria è opportuno usare **DROP AVAILABILITY GROUP** solo in casi di emergenza, poiché, se si elimina un gruppo di disponibilità, quest'ultimo viene portato offline. Se si elimina il gruppo di disponibilità da una replica secondaria, la replica primaria non è in grado di determinare se lo stato è passato a **OFFLINE** a causa della perdita del quorum, di un failover forzato o di un comando **DROP AVAILABILITY GROUP**. La replica primaria passa allo stato **RESTORING** per impedire una possibile situazione split-brain. Per altre informazioni, vedere [How It Works: DROP AVAILABILITY GROUP Behaviors](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (Funzionamento: comportamenti di DROP AVAILABILITY GROUP) nel blog del Supporto Tecnico di SQL Server.  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Autorizzazioni  
 Sono necessarie l'autorizzazione **ALTER AVAILABILITY GROUP** nel gruppo di disponibilità, l'autorizzazione **CONTROL AVAILABILITY GROUP** permission, l'autorizzazione **ALTER ANY AVAILABILITY GROUP** o l'autorizzazione **CONTROL SERVER**. Per eliminare un gruppo di disponibilità non ospitato dall'istanza del server locale, è necessaria l'autorizzazione **CONTROL SERVER** o **CONTROL** in tale gruppo di disponibilità.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eliminato il gruppo di disponibilità `AccountsAG`.  
  
```  
DROP AVAILABILITY GROUP AccountsAG;  
```  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   [How It Works: DROP AVAILABILITY GROUP Behaviors](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (Funzionamento: comportamenti di DROP AVAILABILITY GROUP) nel blog del Supporto Tecnico di SQL Server  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [Rimuovere un gruppo di disponibilità &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
  
