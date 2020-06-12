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
ms.openlocfilehash: f6e1326a00a940b488487f9d602595e6528cb048
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/26/2020
ms.locfileid: "83856534"
---
# <a name="delete-objects"></a>Elimina oggetti
  Utilizzare questa finestra di dialogo per eliminare un database o un oggetto di database.  
  
## <a name="ui-element-list"></a>Elenco elementi dell'interfaccia utente  
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
  
  
