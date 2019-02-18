---
title: Limitazioni per Stretch Database | Microsoft Docs
ms.date: 06/14/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, limitations
- Stretch Database, blocking issues
- limitations (Stretch Database)
- blocking issues (Stretch Database)
ms.assetid: 2b1fbec1-7859-44fc-8417-724fc57a59c0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 90e6bbd804d69af00d8e006d3ca363e09dacd8c3
ms.sourcegitcommit: ec1f01b4bb54621de62ee488decf9511d651d700
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56240765"
---
# <a name="limitations-for-stretch-database"></a>Limitazioni per Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Informazioni sulle limitazioni per le tabelle basate sull'estensione e sulle limitazioni che attualmente impediscono l'abilitazione dell'estensione per una tabella.  
  
##  <a name="Caveats"></a> Limitazioni per le tabelle abilitate per l'estensione  
  
Le tabelle abilitate per l'estensione presentano le limitazioni seguenti.  
  
### <a name="constraints"></a>Vincoli  
-   L'univocità non viene applicata per i vincoli UNIQUE e PRIMARY KEY nella tabella di Azure che contiene i dati migrati.  
  
### <a name="dml-operations"></a>Operazioni DML  
-   Non è possibile aggiornare o eliminare righe che sono state migrate o le righe idonee per la migrazione in una tabella abilitata per l'estensione o una vista che include tabelle basate sull'estensione.  
  
-   Non è possibile inserire righe in una tabella abilitata per l'estensione in un server collegato.  
  
### <a name="indexes"></a>Indici  
-   Non è possibile creare un indice per una vista che include tabelle abilitate per l'estensione.  
  
-   I filtri sugli indici [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non vengono propagati alla tabella remota.  
  
##  <a name="Limitations"></a> Limitazioni che attualmente impediscono l'abilitazione dell'estensione per una tabella  
   
 Gli elementi seguenti attualmente impediscono l'abilitazione dell'estensione per una tabella.  
  
 ### <a name="table-properties"></a>Proprietà tabella  
-   Tabelle con più di 1.023 colonne o più di 998 indici  
  
-   Tabelle FileTable o che contengono dati FILESTREAM  
  
-   Tabelle replicate o che usano attivamente il rilevamento delle modifiche o Change Data Capture  
  
-   Tabelle con ottimizzazione per la memoria  
  
### <a name="data-types"></a>Tipi di dati  
-   text, ntext e image  
  
-   TIMESTAMP  
  
-   sql_variant  
  
-   XML  
  
-   Tipi di dati CLR tra cui geometry, geography, hierarchyid e tipi CLR definiti dall'utente  
  
 ### <a name="column-types"></a>Tipi di colonna  
 -   COLUMN_SET  
  
-   Colonne calcolate  
  
### <a name="constraints"></a>Vincoli  
-   Vincoli predefiniti e vincoli check  
  
-   Vincoli di chiave esterna che fanno riferimento alla tabella. In una relazione padre-figlio (ad esempio, Order e Order_Detail), è possibile abilitare l'estensione per la tabella figlio (Order_Detail) ma non per la tabella padre (Order).  
  
### <a name="indexes"></a>Indici  
-   Indici full-text  
  
-   Indici XML  
  
-   Indici spaziali  
  
-   Viste indicizzate che fanno riferimento alla tabella  
  
## <a name="see-also"></a>Vedere anche  
 [Identificare i database e le tabelle per Estensione database eseguendo Stretch Database Advisor](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)   
 [Abilitare Stretch Database per un database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Enable Stretch Database for a table (Abilitare Estensione database per una tabella)](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
