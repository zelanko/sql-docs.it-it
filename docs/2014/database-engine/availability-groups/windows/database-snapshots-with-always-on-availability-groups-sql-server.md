---
title: Snapshot del database con Gruppi di disponibilità AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 7432da1c-ce2f-4cd9-af41-54c97744166b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cba02aa87e800391ffba3c791c1ee4341462c3f8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62814657"
---
# <a name="database-snapshots-with-alwayson-availability-groups-sql-server"></a>Snapshot del database con gruppi di disponibilità AlwaysOn (SQL Server)
  È possibile creare uno snapshot del database in un qualsiasi database primario o secondario in un gruppo di disponibilità. Il ruolo di replica deve essere PRIMARY o SECONDARY, non nello stato di RESOLVING.  
  
 È consigliabile uno stato di sincronizzazione del database corrispondente a SYNCHRONIZING o SYNCHRONIZED quando si crea uno snapshot del database. È tuttavia possibile creare gli snapshot del database anche se lo stato della sincronizzazione del database è NOT SYNCHRONIZING.  
  
 Uno snapshot del database in una replica secondaria deve continuare a funzionare anche se la replica è disconnessa (DISCONNECTED) dalla replica primaria.  
  
 Alcune condizioni di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] causano il riavvio del database di origine e degli snapshot del database, disconnettendo temporaneamente gli utenti. Tali condizioni sono descritte di seguito:  
  
-   La replica primaria cambia i ruoli, perché la replica primaria corrente viene portata offline e poi online sulla stessa istanza del server o perché si verifica il failover del gruppo di disponibilità.  
  
-   Il database passa al ruolo secondario.  
  
 Se si verifica il failover della replica di disponibilità che ospita gli snapshot del database, gli snapshot del database rimangono sull'istanza del server dove sono stati creati. Gli utenti possono continuare a utilizzare gli snapshot dopo il failover. Se le prestazioni sono una preoccupazione, è consigliabile creare snapshot del database solo sui database secondari ospitati da una replica secondaria configurata per la modalità failover manuale.  Se si esegue il failover manuale del gruppo di disponibilità in questa replica secondaria, è possibile creare un nuovo set di snapshot del database su un'altra replica secondaria, reindirizzare i client ai nuovi snapshot del database ed eliminare tutti gli snapshot del database dai nuovi database primari.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Snapshot del database &#40;SQL Server&#41;](../../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
