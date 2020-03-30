---
title: Impostazioni filtro (Esplora oggetti ed Esplora utilità)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.common.filtersettings.f1
- sql13.ag.job.filtersettings.f1
ms.assetid: 4aab04bc-e1ab-4d4b-ab74-b287fc805bc2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fe88e33261171b0c1584c89561e9fac2f081b816
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75257178"
---
# <a name="filter-settings-object-explorer-and-utility-explorer"></a>Impostazioni filtro (Esplora oggetti ed Esplora utilità)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Utilizzare questa finestra di dialogo per specificare un filtro. Un filtro consente di configurare Esplora oggetti e Gestione Utilità in modo da visualizzare solo gli elementi che soddisfano determinati criteri. È possibile, ad esempio, utilizzare un filtro per visualizzare solo i processi i cui nomi contengono la parola "Manutenzione". L'intestazione della finestra di dialogo **Impostazioni filtro** contiene il nome del server e può contenere anche il nome del database.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
**Proprietà**  
Consente di visualizzare la proprietà in base a cui applicare il filtro.  
  
**Operatore**  
Consente di selezionare il modo in cui il valore viene applicato alla proprietà dal filtro. Sono disponibili le opzioni seguenti:  
  
-   **Uguale a**  
  
    Il filtro visualizza gli elementi in cui la proprietà e il valore corrispondono esattamente.  
  
-   **Contiene**  
  
    Il filtro visualizza gli elementi in cui la proprietà contiene il valore. La proprietà può contenere altro testo.  
  
-   **Non contiene**  
  
    Il filtro visualizza gli elementi in cui la proprietà non contiene il valore.  
  
-   **Minore di**  
  
    Questo operatore è disponibile per le date e visualizza gli elementi la cui data è precedente al valore immesso.  
  
-   **Minore o uguale a**  
  
    Questo operatore è disponibile per le date e visualizza gli elementi la cui data corrisponde o è precedente al valore immesso.  
  
-   **Maggiore di**  
  
    Questo operatore è disponibile per le date e visualizza gli elementi la cui data è successiva al valore immesso.  
  
-   **Maggiore o uguale a**  
  
    Questo operatore è disponibile per le date e visualizza gli elementi la cui data corrisponde o è successiva al valore immesso.  
  
-   **Compreso tra**  
  
    Questo operatore è disponibile per le date e visualizza gli elementi la cui data è compresa tra due date immesse. Per aggiungere un'altra riga che consenta l'immissione della seconda data selezionare **Compreso tra** e premere TAB.  
  
-   **Non compreso tra**  
  
    Questo operatore è disponibile per le date e visualizza gli elementi la cui data è precedente o successiva alle due date immesse. Per aggiungere un'altra riga che consenta l'immissione della seconda data selezionare **Non compreso tra** e premere TAB per uscire dalla colonna **Operatore** .  
  
**Valore**  
Consente di digitare il valore da confrontare con la proprietà. Fare clic sulla freccia a discesa per visualizzare un calendario che consente di selezionare la data.  
  
**Cancella filtro**  
Consente di eliminare tutte le impostazioni correnti del filtro.  
  
## <a name="see-also"></a>Vedere anche  
[Utilizzo di SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
[Panoramica dell'Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
