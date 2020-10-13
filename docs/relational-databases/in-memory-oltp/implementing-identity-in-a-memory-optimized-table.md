---
title: Implementazione di IDENTITY in una tabella con ottimizzazione per la memoria | Microsoft Docs
description: Informazioni su IDENTITY nelle tabelle ottimizzate per la memoria in SQL Server. Le tabelle ottimizzate per la memoria supportano IDENTITY per un valore di inizializzazione e di incremento pari a uno.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5aecab53a9144d5254eb85190f7652dbe090bf82
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869120"
---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>Implementazione di IDENTITY in una tabella con ottimizzazione per la memoria
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

IDENTITY è supportato in una tabella ottimizzata per la memoria, purché il valore di inizializzazione e incremento siano entrambi pari a 1 (ovvero l'impostazione predefinita). Le colonne Identity con la definizione di IDENTITY(x, y) dove x != 1 o y != 1 non sono supportate nelle tabelle ottimizzate per la memoria.   
    
Per aumentare il valore di inizializzazione IDENTITY, inserire una nuova riga con un valore esplicito per la colonna Identity, usando l'opzione della sessione `SET IDENTITY_INSERT table_name ON`. Con l'inserimento della riga, il valore di inizializzazione IDENTITY viene cambiato nel valore inserito in modo esplicito più 1. Ad esempio, per aumentare il valore di inizializzazione a 1000, inserire una riga con valore 999 nella colonna Identity. I valori Identity generati inizieranno quindi da 1000.     
  
## <a name="see-also"></a>Vedere anche  
 [Migrazione a OLTP in memoria](./plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)  
  
