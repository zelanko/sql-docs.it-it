---
description: Nuova pianificazione processo - Proprietà pianificazione processo
title: Nuova pianificazione processo - Proprietà pianificazione processo
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.scheduleproperties.f1
- sql13.swb.maint.editrecurringjobsched.f1
ms.assetid: 5c0b1bc9-dd87-49cc-b0dd-75d0d922b177
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 68fde830b44cfb922c9908a75c62c4fbb86d3001
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97402557"
---
# <a name="new-job-schedule---job-schedule-properties"></a>Nuova pianificazione processo - Proprietà pianificazione processo
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di SQL di Azure](/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita di SQL di Azure e SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Utilizzare questa pagina per visualizzare e modificare le proprietà della pianificazione.  
  
## <a name="options"></a>Opzioni  
**Nome**  
Consente di digitare un nuovo nome per la pianificazione.  
  
**Processi nella pianificazione**  
Consente di visualizzare i processi che utilizzano la pianificazione.  
  
**Tipo pianificazione**  
Consente di selezionare il tipo di pianificazione.  
  
**Enabled**  
Consente di abilitare o disabilitare la pianificazione.  
  
## <a name="recurring-schedule-types-options"></a>Opzioni relative ai tipi di pianificazione periodica  
**Ricorrenza**  
Consente di selezionare l'intervallo in base al quale ripetere la pianificazione.  
  
**Ogni**  
Consente di selezionare il numero di giorni o di settimane quale intervallo di esecuzione delle pianificazioni. Questa opzione non è disponibile per le pianificazioni periodiche con frequenza mensile.  
  
**Lunedì**  
Consente di impostare l'esecuzione del processo ogni lunedì. Questa opzione è disponibile solo per le pianificazioni periodiche con frequenza settimanale.  
  
**Martedì**  
Consente di impostare l'esecuzione del processo ogni martedì. Questa opzione è disponibile solo per le pianificazioni periodiche con frequenza settimanale.  
  
**Mercoledì**  
Consente di impostare l'esecuzione del processo ogni mercoledì. Questa opzione è disponibile solo per le pianificazioni periodiche con frequenza settimanale.  
  
**Giovedì**  
Consente di impostare l'esecuzione del processo ogni giovedì. Questa opzione è disponibile solo per le pianificazioni periodiche con frequenza settimanale.  
  
**Venerdì**  
Consente di impostare l'esecuzione del processo ogni venerdì. Questa opzione è disponibile solo per le pianificazioni periodiche con frequenza settimanale.  
  
**Sabato**  
Consente di impostare l'esecuzione del processo ogni sabato. Questa opzione è disponibile solo per le pianificazioni periodiche con frequenza settimanale.  
  
**Domenica**  
Consente di impostare l'esecuzione del processo ogni domenica. Questa opzione è disponibile solo per le pianificazioni periodiche con frequenza settimanale.  
  
**Day**  
Consente di selezionare il giorno del mese in cui eseguire la pianificazione. Questa opzione è disponibile solo per le pianificazioni periodiche con frequenza mensile.  
  
**ogni**  
Consente di selezionare il numero di mesi tra una pianificazione e l'altra. Questa opzione è disponibile solo per le pianificazioni periodiche con frequenza mensile.  
  
**Ogni**  
Consente di specificare una pianificazione per un giorno specifico di una determinata settimana del mese. Questa opzione è disponibile solo per le pianificazioni periodiche con frequenza mensile.  
  
**Una sola volta alle**  
Consente di impostare l'ora per l'esecuzione giornaliera di un processo.  
  
**Ogni**  
Consente di impostare il numero di ore, di minuti o secondi tra le occorrenze.  
  
**Data inizio**  
Consente di impostare la data iniziale di validità per la pianificazione.  
  
**Data fine**  
Consente di impostare la data finale di validità per la pianificazione.  
  
**Nessuna data di fine**  
Consente di specificare una validità illimitata per la pianificazione.  
  
## <a name="one-time-schedule-types-options"></a>Opzioni relative ai tipi di pianificazione da eseguire una sola volta  
**Data**  
Selezionare la data di esecuzione del processo.  
  
**Time**  
Selezionare l'ora di esecuzione del processo.  
  
## <a name="see-also"></a>Vedere anche  
[Creazione e collegamento di pianificazioni ai processi](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[Pianificare un processo](../../ssms/agent/schedule-a-job.md)  
