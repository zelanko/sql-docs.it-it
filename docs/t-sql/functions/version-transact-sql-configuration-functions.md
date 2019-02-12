---
title: '@@VERSION (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/20/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@VERSION'
- '@@VERSION_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@VERSION function'
- current SQL Server installation information
- versions [SQL Server], @@VERSION
- processors [SQL Server], types
ms.assetid: 385ba80e-7c28-41a5-9cdb-5648f3785983
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3f5b04781959218d9044f1bf032156ce6ec65946
ms.sourcegitcommit: 97340deee7e17288b5eec2fa275b01128f28e1b8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/30/2019
ms.locfileid: "55420959"
---
# <a name="x40x40version---transact-sql-configuration-functions"></a>&#x40;&#x40;Version - Funzioni di configurazione di Transact SQL
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce informazioni sul sistema e sulla build dell'installazione corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
@@VERSION  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 I risultati di @@VERSION vengono presentati come una stringa di tipo nvarchar. Per recuperare i singoli valori delle proprietà, è possibile usare la funzione [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md).  
  
 Per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono restituite le informazioni seguenti.  
  
-   Versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Architettura del processore  
  
-   Data di compilazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Dichiarazione di copyright  
  
-   Edizione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]   
  
-   Versione del sistema operativo  
  
 Per [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] vengono restituite le informazioni seguenti.  
  
-   Edizione- "Microsoft SQL Azure"  
  
-   Livello del prodotto- "(RTM)"  
  
-   Versione del prodotto  
  
-   Data di compilazione  
  
-   Dichiarazione di copyright  

> [!NOTE]  
> Esiste un problema noto a causa del quale la versione del prodotto segnalata da @@VERSION non è corretta per il database SQL di Azure. La versione del motore di database di SQL Server eseguita dal database SQL di Azure è sempre più avanti rispetto alla versione locale di SQL Server e include le correzioni della sicurezza più recenti. Questo significa che il livello di patch è sempre corrispondente o posteriore a quello della versione locale di SQL Serve, e che le funzionalità più recenti disponibili in SQL Server sono disponibili nel database SQL di Azure.
>
> Per determinare a livello di codice l'edizione del motore, usare SELECT SERVERPROPERTY('EngineEdition'). Questa query restituirà '5' per database singoli/pool elastici e '8' per le istanze gestite nel database SQL di Azure. 
>
> La documentazione verrà aggiornato una volta risolto il problema.

  
## <a name="examples"></a>Esempi  
  
### <a name="a-return-the-current-version-of-includessnoversionincludesssnoversion-mdmd"></a>A: Restituire la versione corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Nell'esempio seguente vengono restituite le informazioni sulla versione relative all'installazione corrente.  
  
```  
SELECT @@VERSION AS 'SQL Server Version';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-return-the-current-version-of-includessdwincludesssdw-mdmd"></a>b. Restituire la versione corrente di [!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
  
```  
SELECT @@VERSION AS 'SQL Server PDW Version';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
  

