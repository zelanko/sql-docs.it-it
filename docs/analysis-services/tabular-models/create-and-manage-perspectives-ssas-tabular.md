---
title: Creare e gestire prospettive nei modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 962b6b90de6d95107d1a4cdd3484a44205afb630
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53071848"
---
# <a name="create-and-manage-perspectives"></a>Creare e gestire prospettive 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Le prospettive consentono di definire subset visualizzabili di un modello in grado di offrire punti di vista mirati, specifici di un'attività aziendale o di un'applicazione del modello. Nelle attività di questo argomento vengono descritte le modalità di creazione e gestione delle prospettive tramite la finestra di dialogo **Prospettive** in Progettazione modelli.  
  
## <a name="tasks"></a>Attività  
 Per creare prospettive si utilizzerà la finestra di dialogo **Prospettive** in cui è possibile aggiungere, modificare, eliminare, copiare e visualizzare prospettive. Per visualizzare la finestra di dialogo **Prospettive** , in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic sul menu **Modello** , quindi scegliere **Prospettive**.  
  
###  <a name="bkmk_add"></a> Per aggiungere una prospettiva  
  
-   Per aggiungere una nuova prospettiva, fare clic su **Nuova prospettiva**. È possibile selezionare e deselezionare gli oggetti campo da includere e fornire un nome per la nuova prospettiva.  
  
     Se si crea una prospettiva vuota con tutti i campi dell'oggetto campo, un utente che utilizza questa prospettiva visualizzerà un elenco di campi vuoto. Le prospettive devono contenere almeno una tabella e una colonna.  
  
###  <a name="bkmk_edit"></a> Per modificare una prospettiva  
  
-   Per modificare una prospettiva, selezionare e deselezionare i campi nella colonna della prospettiva, che aggiunge e rimuove gli oggetti campo dalla prospettiva.  
  
###  <a name="bkmk_rename"></a> Per rinominare una prospettiva  
  
-   Quando passa il mouse sull'intestazione di colonna della prospettiva (il nome della prospettiva), il **Rinomina** viene visualizzato il pulsante. Per rinominare la prospettiva, fare clic su **Rinomina**, quindi immettere un nuovo nome o modificare quello esistente.  
  
###  <a name="bkmk_delete"></a> Per eliminare una prospettiva  
  
-   Quando passa il mouse sull'intestazione di colonna della prospettiva (il nome della prospettiva), il **eliminare** viene visualizzato il pulsante. Per eliminare la prospettiva, fare clic sul pulsante **Elimina** , quindi scegliere **Sì** nella finestra di conferma.  
  
###  <a name="bkmk_copy"></a> Per copiare una prospettiva  
  
-   Quando passa il mouse sull'intestazione di colonna della prospettiva, la **copia** viene visualizzato il pulsante. Per creare una copia di tale prospettiva, fare clic sul pulsante **Copia** . Una copia della prospettiva selezionata viene aggiunta come nuova prospettiva a destra delle prospettive esistenti. Il nome della nuova prospettiva viene ereditato dalla prospettiva copiata e alla fine del nome viene accodata un'annotazione *- Copy* . Se, ad esempio, una copia del *vendite* prospettiva viene creata, la nuova prospettiva viene denominata *vendite - copia*.  
  
## <a name="see-also"></a>Vedere anche  
 [Prospettive](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Gerarchie](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)  
  
  
