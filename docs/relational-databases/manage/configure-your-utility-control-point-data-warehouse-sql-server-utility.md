---
title: Configurare il data warehouse del punto di controllo dell'utilità (Utilità SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: c2c6f050-8cdb-4b8e-ad38-4aae0a949847
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f71e3ce611c8bf4b9ecfdd0cdafdafe4ca771874
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68115472"
---
# <a name="configure-your-utility-control-point-data-warehouse-sql-server-utility"></a>Configurazione del data warehouse del punto di controllo dell'utilità (Utilità SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  I dati raccolti dalle istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono archiviati nel data warehouse di gestione dell'utilità. Il nome del file del data warehouse di gestione dell'utilità è sysutility_mdw.  
  
 È possibile configurare il periodo di memorizzazione dei dati in tale data warehouse. Per altre informazioni, vedere [Amministrazione utilità &#40;Utilità SQL Server&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d).  
  
 Le impostazioni di configurazione seguenti non sono configurabili in questa versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Nome del data warehouse di gestione dell'utilità: Sysutility_mdw.  
  
-   Frequenza di caricamento del set di raccolta: ogni 15 minuti.  
  
 La directory dell'utilità UMDW è configurabile: \<Unità di sistema>:\Programmi\Microsoft SQL Server\MSSQL10_50.<Nome_UCP>\MSSQL\Data\\, dove \<Unità di sistema> è in genere l'unità C:\. Il file di log, Sysutility_mdw_\<GUIDA>_LOG, si trova nella stessa directory.  
  
> [!NOTE]  
>  È possibile modificare la posizione del file data warehouse di gestione dell'utilità (UMDW) sysutility_mdw utilizzando i comandi collega/scollega o l'istruzione ALTER DATABASE. È consigliabile utilizzare l'istruzione ALTER DATABASE. Per altre informazioni, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
