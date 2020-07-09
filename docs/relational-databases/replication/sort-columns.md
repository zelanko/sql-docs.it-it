---
title: Ordina colonne | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.sortcolumns.f1
ms.assetid: 66b44b6c-10a5-4e3f-a97b-7568609c88ac
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 0840b390e6a4771b5e92be75e560fb22f1822e05
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728254"
---
# <a name="sort-columns"></a>Ordina colonne
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  La finestra di dialogo **Ordina colonne** consente di ordinare le griglie in Monitoraggio replica in base a una o più colonne. È anche possibile eseguire l'ordinamento in base a una singola colonna facendo clic sull'intestazione di colonna nella griglia di Monitoraggio replica. Per ordinare, ad esempio, le sottoscrizioni nella scheda **Tutte le sottoscrizioni** in base allo stato e quindi al tipo di connessione, eseguire la procedura seguente:  
  
1.  Nella prima riga della griglia selezionare **Stato** nella colonna **Nome colonna** e un valore nella colonna **Ordinamento**  
  
2.  Nella seconda riga della griglia selezionare **Tipo di connessione** nella colonna **Nome colonna** e un valore nella colonna **Ordinamento** .  

## <a name="options"></a>Opzioni  
 **Nome colonna**  
 Nome della colonna in base a cui si desidera eseguire l'ordinamento. È possibile eseguire l'ordinamento in base a una o più colonne. Non è possibile eseguire l'ordinamento in base alle colonne **Prestazioni medie correnti** o **Prestazioni peggiori correnti** nella scheda **Pubblicazioni** , a causa della modalità con cui vengono calcolati i valori di queste colonne.  
  
 **Ordinamento**  
 Consente di specificare un valore **Crescente** o **Decrescente**.  
  
 **Cancella tutto**  
 Consente di rimuovere tutte le righe dalla griglia di ordinamento. Per rimuovere una singola riga, selezionarla e premere Canc.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
