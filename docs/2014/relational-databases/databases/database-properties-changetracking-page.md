---
title: Proprietà database (pagina Rilevamento modifiche) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.changetracking.f1
ms.assetid: 9b929640-bc62-449b-9b06-b5a77b8cf372
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 926f6227d5a3a2e11dffbf4b9f080b1fc5ec35a2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62871854"
---
# <a name="database-properties-changetracking-page"></a>Proprietà database (pagina ChangeTracking)
  Utilizzare questa pagina per visualizzare o modificare le impostazioni di rilevamento delle modifiche per il database selezionato. Per altre informazioni sulle opzioni disponibili in questa pagina, vedere [Abilitare e disabilitare il rilevamento delle modifiche &#40;SQL Server&#41;](../track-changes/enable-and-disable-change-tracking-sql-server.md).  
  
## <a name="options"></a>Opzioni  
 **Rilevamento delle modifiche**  
 Consente di abilitare o disabilitare il rilevamento delle modifiche per il database.  
  
 Per abilitare il rilevamento delle modifiche, è necessario disporre dell'autorizzazione per modificare il database.  
  
 L'impostazione del valore su **True** consente di impostare un'opzione del database che consente l'abilitazione del rilevamento delle modifiche nelle singole tabelle.  
  
 È anche possibile configurare il rilevamento delle modifiche usando [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql).  
  
 **Periodo di conservazione**  
 Specifica il periodo minimo di conservazione delle informazioni sul rilevamento delle modifiche nel database. I dati vengono rimossi solo se il valore **Pulizia automatica**è impostato su **True**.  
  
 Il valore predefinito è 2.  
  
 **Unità di misura del periodo di memorizzazione**  
 Specifica le unità di misura per il valore Periodo di memorizzazione. È possibile selezionare **Giorni**, **Ore**o **Minuti**. Il valore predefinito è **Giorni**.  
  
 Il periodo di memorizzazione minimo è 1 minuto. Non esiste un periodo di memorizzazione massimo.  
  
 **Pulizia automatica**  
 Indica se le informazioni di rilevamento delle modifiche vengono rimosse automaticamente una volta trascorso il periodo di memorizzazione specificato.  
  
 L'abilitazione di **Pulizia automatica** reimposta i precedenti periodi di memorizzazione personalizzati al periodo di memorizzazione predefinito di 2 giorni.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  
