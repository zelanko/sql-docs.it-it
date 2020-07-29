---
title: Finestra di dialogo Salva (non consentito)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.table.tablerecreatenosave.f1
ms.assetid: 7efda8e3-739f-4c97-a497-b8808a0acbea
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: b6bd4471f14d662b6167c00d599eccf61b7dcced
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86010648"
---
# <a name="save-not-permitted-dialog-box"></a>Finestra di dialogo Salva (non consentito)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
La finestra di dialogo **Salva** (non consentito) avvisa che il salvataggio delle modifiche non è consentito perché prima devono essere eliminate e ricreate le tabelle elencate.  
  
Per le azioni seguenti può essere necessario ricreare una tabella:  
  
-   Aggiunta di una nuova colonna a metà tabella  
  
-   Eliminazione di una colonna  
  
-   Modifica dell'ammissione di valori Null nella colonna  
  
-   Modifica dell'ordine delle colonne  
  
-   Modifica del tipo di dati di una colonna  
  
Per modificare questa opzione, scegliere **Opzioni** dal menu **Strumenti**, espandere **Finestre di progettazione**, quindi fare clic su **Progettazione tabelle e Progettazione database**. Selezionare o deselezionare la casella di controllo **Impedisci il salvataggio delle modifiche per cui è necessario ricreare la tabella** .  
  
