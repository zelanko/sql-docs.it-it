---
title: Eliminare oggetti | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.deleteobjects.f1
helpviewer_keywords:
- Delete Objects dialog box
ms.assetid: 49541441-179c-40d3-ba0c-01bcae545984
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 35ce645577ca276f4f5ec6a5792d27859369a821
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65102761"
---
# <a name="delete-objects"></a>Elimina oggetti
  Utilizzare questa finestra di dialogo per eliminare un database o un oggetto di database.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **Oggetto da eliminare**  
 Consente di visualizzare i nomi, i tipi, i proprietari e lo stato degli oggetti da eliminare, nonché gli eventuali messaggi relativi agli errori verificatisi durante l'esecuzione.  
  
> [!NOTE]  
>  L'esecuzione dell'opzione **Elimina** su un database equivale all'esecuzione di DROP DATABASE in [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Mostra dipendenze**  
 Fare clic su questo pulsante per visualizzare sia gli oggetti che dipendono dall'oggetto attualmente selezionato che gli oggetti dal quale dipende l'oggetto corrente (dipendenza verso l'alto e verso il basso). Le informazioni visualizzate nella finestra di dialogo **Mostra dipendenze** sono di sola lettura.  
  
> [!NOTE]  
>  Il pulsante **Mostra dipendenze** non viene visualizzato per tutti i tipi di oggetti di database. Per visualizzare le dipendenze quando il pulsante **Mostra dipendenze** non è disponibile, fare clic sull'oggetto con il pulsante destro del mouse in Esplora oggetti e scegliere **Visualizza dipendenze**.  
  
 **Elimina informazioni di cronologia di backup e ripristino per i database**  
 Questa casella di controllo viene visualizzata solo quando viene eliminato un database e comporta l'eliminazione dal database **msdb** della cronologia di backup e ripristino del database eliminato.  
  
 **Chiudi connessioni esistenti**  
 Questa casella di controllo viene visualizzata solo quando viene eliminato un database e interrompe le connessioni al database eliminato.  
  
  
