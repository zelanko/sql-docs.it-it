---
title: Massimo grado di parallelismo e gestione basata su criteri
description: Viene descritta la configurazione di criteri per verificare il valore dell'opzione max degree of parallelism per la gestione basata su criteri per SQL Server.
ms.custom: seo-lt-2019
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a03a0236c177605bf5041e92ea9c19708d5bc9ae
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "75776368"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>Impostazione dell'opzione relativa al massimo grado di parallelismo per ottenere prestazioni ottimali
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questa regola consente di determinare se l'opzione relativa al massimo grado di parallelismo (MAXDOP) sia un valore maggiore di 8. L'impostazione di questa opzione su un valore maggiore provoca in genere un utilizzo indesiderato delle risorse e una riduzione delle prestazioni.  
  
## <a name="best-practice-recommendations"></a>Indicazioni sulle procedure consigliate  
 L'opzione di configurazione max degree of parallelism (MAXDOP) consente di controllare il numero di processori usati per l'esecuzione di una query in un piano parallelo. Questa opzione determina il numero di thread usati per gli operatori del piano di query che eseguono il lavoro in parallelo. A seconda del fatto che SQL Server sia installato in un computer SMP (Symmetric Multiprocessing), in un computer NUMA (Non-Uniform Memory Access) o in processori abilitati per l'hyper-threading, è necessario configurare l'opzione max degree of parallelism in modo appropriato. 
 
 Le raccomandazioni per configurare MAXDOP dipendono dalla versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in uso. Per le linee guida specifiche della versione, vedere [Configurare l'opzione di configurazione del server max degree of parallelism](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines) e configurare i criteri per verificare di conseguenza il valore di max degree of parallelism.     
  
## <a name="for-more-information"></a>Per ulteriori informazioni  
 [Indicazioni e linee guida per l'opzione di configurazione "max degree of parallelism" in SQL Server](https://go.microsoft.com/fwlink/?linkid=117786)    
 [Configurare l'opzione di configurazione del server max degree of parallelism](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)     
  
