---
title: Aggiungere una tabella a un modello tabulare di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 224df75c15acf560c7eadc70fe91fbbc2b0396d9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207876"
---
# <a name="add-a-table"></a>Aggiungere una tabella
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Questo articolo descrive come aggiungere una tabella da un'origine dati da cui sono stati importati precedentemente i dati nel modello. Per aggiungere una tabella dalla stessa origine dati, è possibile utilizzare la connessione all'origine dati esistente. È consigliabile utilizzare sempre una sola connessione in caso di importazione di un qualsiasi numero di tabelle da un'unica origine dati.  
  
### <a name="to-add-a-table-from-an-existing-data-source"></a>Per aggiungere una tabella da un'origine dati esistente  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]scegliere **Connessioni esistenti** dal menu **Modello**.  
  
2.  Nella pagina **Connessioni esistenti** selezionare la connessione all'origine dati contenente la tabella da aggiungere, quindi fare clic su **Apri**.  
  
3.  Nella pagina **Selezione tabelle e viste** selezionare la tabella dall'origine dati che si desidera aggiungere al modello.  
  
    > [!NOTE]  
    >  Nella pagina **Selezione tabelle e viste** non verranno mostrate le tabelle importate in precedenza come selezionate.  Se si seleziona una tabella che è stata precedentemente importata tramite questa connessione e a cui non è stato assegnato un nome descrittivo diverso, verrà accodato 1 al nome utilizzato. Non è necessario selezionare di nuovo tutte le tabelle importate precedentemente tramite questa connessione.  
  
4.  Se necessario, usare **Visualizza anteprima e applica filtro** per selezionare solo determinate colonne o per applicare filtri ai dati da importare.  
  
5.  Fare clic su **Fine** per importare la nuova tabella.  
  
> [!NOTE]  
>  Se si importano più tabelle contemporaneamente da una sola origine dati, tutte le relazioni tra tali tabelle nell'origine saranno create automaticamente nel modello. In caso di aggiunta di una tabella in un secondo momento, potrebbe essere tuttavia necessario creare manualmente le relazioni nel modello tra le tabelle appena aggiunte e quelle importate in precedenza.  
  
## <a name="see-also"></a>Vedere anche  
 [Importazione dei dati](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [Eliminare una tabella](../../analysis-services/tabular-models/delete-a-table-ssas-tabular.md)  
  
  
