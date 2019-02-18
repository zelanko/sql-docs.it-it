---
title: Identificare i database e le tabelle per Stretch Database | Microsoft Docs
ms.date: 10/30/2017
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, identifying databases
- Stretch Database, identifying tables
- identifying databases for Stretch Database
- identifying tables for Stretch Database
ms.assetid: 81bd93d8-eef8-4572-88d7-5c37ab5ac2bf
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cc6869720018e6787c915fd56e5810b319c651de
ms.sourcegitcommit: ec1f01b4bb54621de62ee488decf9511d651d700
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56240745"
---
# <a name="identify-databases-and-tables-for-stretch-database-with-data-migration-assistant"></a>Identificare i database e le tabelle per Stretch Database con Data Migration Assistant
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Per identificare i database e le tabelle candidati per Stretch Database e i problemi di blocco potenziali, scaricare ed eseguire Microsoft Data Migration Assistant.
  
## <a name="get-data-migration-assistant"></a>Ottenere Data Migration Assistant
 Scaricare e installare Data Migration Assistant da [qui](https://www.microsoft.com/download/details.aspx?id=53595). Questo strumento non è incluso nel supporto di installazione di SQL Server.  
  
## <a name="run-data-migration-assistant"></a>Eseguire Data Migration Assistant  
  
1.  Eseguire Microsoft Data Migration Assistant.  

2.  Creare un nuovo progetto di tipo **Valutazione** e assegnargli un nome.

3.  Selezionare **SQL Server** come **Source server type** (Tipo server di origine) e **Target server type** (Tipo server di destinazione).

4.  Selezionare **Crea**. 

5. Nella pagina **Options** (Opzioni) (passaggio 1) selezionare **New features recommendation** (Nuove funzionalità raccomandate). Facoltativamente, deselezionare l'opzione **Compatibility issues** (Problemi di compatibilità).

6.  Nella pagina **Select sources** (Seleziona origini) (passaggio 2) connettersi a un server, selezionare un database e quindi selezionare **Aggiungi**.

7.  Selezionare **Start Assessment** (Avvia valutazione).

## <a name="review-the-results"></a>Controllare i risultati  
  
1.  Al termine dell'analisi, nella pagina **Review results** (Verifica risultati) (passaggio 3) selezionare l'opzione **Funzionalità consigliate** e quindi selezionare la scheda **Archiviazione**.

2.  Esaminare i consigli relativi a Stretch Database. Ogni consiglio elenca le tabelle per cui Stretch Database potrebbe essere appropriato, insieme a eventuali problemi di blocco potenziali.

## <a name="historical-note"></a>Nota storica
Stretch Database Advisor era in precedenza un componente di Gestione spazio aggiornamenti di SQL Server 2016. Stretch Database Advisor doveva essere eseguito separatamente.

Con il rilascio di Data Migration Assistant, che sostituisce ed estende Gestione spazio aggiornamenti, la funzionalità di Stretch Database Advisor è incorporata nel nuovo strumento. Non è necessario selezionare alcuna opzione per visualizzare i consigli relativi a Stretch Database. Quando si esegue una valutazione in Data Migration Assistant, i risultati relativi a Stretch Database vengono visualizzati nella scheda **Archiviazione** della finestra **Funzionalità consigliate**.
  
## <a name="next-step"></a>Passaggio successivo  
 Abilitare Stretch Database.  
  
-   Per abilitare Estensione database in un **database**, vedere [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
-   Per abilitare Estensione database in un'altra **tabella**, quando l'estensione è già abilitata nel database, vedere [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md). 
  
## <a name="see-also"></a>Vedere anche  
 [Limitazioni per Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md)   
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Enable Stretch Database for a table (Abilitare Estensione database per una tabella)](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
