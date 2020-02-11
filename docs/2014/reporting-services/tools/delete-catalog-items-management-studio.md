---
title: Elimina elementi catalogo (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.deleteitems.f1
ms.assetid: b0599e01-6dc3-4484-80d4-022a412e0ebd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bacb9387a4026fbf6a41f0b5d9cdd0b77594da97
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66100391"
---
# <a name="delete-catalog-items-management-studio"></a>Elimina elementi catalogo (Management Studio)
  Questa pagina consente di eliminare pianificazioni condivise e definizioni di ruolo.  
  
 Se si elimina una pianificazione condivisa utilizzata da più report e sottoscrizioni, nel server di report vengono create singole pianificazioni per ogni report e sottoscrizione da cui è stata utilizzata in precedenza la pianificazione condivisa. Ogni nuova pianificazione conterrà la data, l'ora e il criterio di occorrenza specificati nella pianificazione condivisa. Si noti che in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è disponibile una funzionalità di gestione centrale delle singole pianificazioni. Se si elimina una pianificazione condivisa, è necessario gestire le informazioni sulla pianificazione per ogni singolo elemento. Prima di eliminare una pianificazione condivisa, utilizzare la pagina [Report](schedule-properties-reports-page.md) per verificare i report da cui attualmente viene utilizzata la pianificazione.  
  
 Per le definizioni di ruolo, è possibile eliminare solo le definizioni non attivamente utilizzate in un'assegnazione di ruolo. Se si tenta di eliminare un ruolo attualmente in uso, tale ruolo non viene eliminato dal server di report e viene visualizzato un messaggio di errore. Se la pagina contiene una singola definizione di ruolo non attualmente in uso, la definizione viene eliminata quando si fa clic su **OK**. Se la pagina contiene più ruoli, non è possibile selezionare i ruoli da conservare o da rimuovere. Facendo clic su **OK**vengono eliminate tutte le definizioni di ruolo non utilizzate.  
  
 Non è possibile annullare un'operazione di eliminazione. Se si desidera recuperare un elemento eliminato, è necessario ricrearlo o ripristinare una copia di backup del database del server di report.  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Indica il nome dell'elemento che si sta eliminando.  
  
 **Tipo**  
 Visualizza il tipo di elemento che si sta eliminando.  
  
 **Proprietario**  
 Visualizza il nome del proprietario. Nella maggior parte dei casi, si tratta di System.  
  
 **Status**  
 Visualizza le informazioni sullo stato dell'operazione di eliminazione.  
  
 **Error (Errore) (Error (Errore)e)**  
 Visualizza un codice se si verifica un errore durante l'eliminazione di un elemento.  
  
## <a name="see-also"></a>Vedere anche  
 [Eliminare un elemento &#40;Management Studio&#41;](delete-an-item-management-studio.md)   
 [Guida sensibile al contesto del server di report in Management Studio](report-server-in-management-studio-f1-help.md)   
 [Creare, modificare ed eliminare pianificazioni](../subscriptions/create-modify-and-delete-schedules.md)  
  
  
