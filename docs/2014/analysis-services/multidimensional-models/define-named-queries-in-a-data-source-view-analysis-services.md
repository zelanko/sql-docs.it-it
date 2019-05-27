---
title: Definire query denominate in una vista origine dati (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- named queries [Analysis Services], creating
- modifying named queries
- data source views [Analysis Services], named queries
ms.assetid: f09ba8aa-950e-4c0d-961e-970de13200be
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bbb792ac4e86ae563f80f35f04854f16501b34a4
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075556"
---
# <a name="define-named-queries-in-a-data-source-view-analysis-services"></a>Definire query denominate in una vista origine dati (Analysis Services)
  Una query denominata è un'espressione SQL rappresentata come tabella. In una query denominata è possibile specificare un'espressione SQL per la selezione di righe e colonne restituite da una o più tabelle in una o più origini dati. Una query denominata è simile a qualsiasi altra tabella in una vista origine dati con righe e relazioni, con la differenza che la query denominata è basata su un'espressione.  
  
 Una query denominata consente di estendere lo schema relazionale delle tabelle esistenti in una vista origine dati senza modificare l'origine dati sottostante. Una serie di query denominate può, ad esempio, essere utilizzata per suddividere una tabella delle dimensioni complessa in tabelle delle dimensioni più piccole e più semplici, da utilizzare nelle dimensioni del database. È inoltre possibile utilizzare una query denominata per unire in join più tabelle di database di una o più origini dati in una singola tabella della vista origine dati.  
  
## <a name="creating-a-named-query"></a>Creazione di una query denominata  
  
> [!NOTE]  
>  Non è possibile aggiungere un calcolo denominato a una query denominata, né basare una query denominata su una tabella contenente un calcolo denominato.  
  
 Quando si crea una query denominata è necessario specificare un nome, la query SQL che restituisce le colonne e i dati per la tabella e, facoltativamente, una descrizione della query denominata. L'espressione SQL può fare riferimento ad altre tabelle della vista origine dati. Dopo avere definito la query denominata, la query SQL in una query denominata viene inviata al provider dell'origine dei dati e convalidata. Se il provider non rileva errori nella query SQL, la colonna viene aggiunta alla tabella.  
  
 È necessario che le tabelle e le colonne a cui fa riferimento la query SQL non siano qualificate oppure siano qualificate solo in base al nome della tabella. Per fare riferimento alla colonna SaleAmount di una tabella, ad esempio, è possibile utilizzare `SaleAmount` o `Sales.SaleAmount` , mentre `dbo.Sales.SaleAmount` genera un errore.  
  
 **Nota** In caso di definizione di una query denominata su un'origine dati [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0, una query denominata contenente una sottoquery e una clausola GROUP BY correlate avrà esito negativo. Per altre informazioni, vedere l'articolo [Internal Error with SELECT Statement Containing Correlated Subquery and GROUP BY](https://support.microsoft.com/kb/274729) (Errore interno con l'istruzione SELECT contenente la sottoquery e GROUP BY correlati) della [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base.  
  
## <a name="add-or-edit-a-named-query"></a>Aggiungere o modificare una query denominata  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto o connettersi al database contenente la vista origine dati in cui si desidera aggiungere una query denominata.  
  
2.  In Esplora soluzioni espandere la cartella **Viste origine dati** , quindi fare doppio clic sulla vista origine dati.  
  
3.  Nel riquadro **Tabelle** o **Diagramma** fare clic con il pulsante destro del mouse su un'area vuota e quindi scegliere **Nuova query denominata**.  
  
4.  Nella finestra di dialogo **Crea query denominata** effettuare le operazioni seguenti:  
  
    1.  Nella casella di testo **Name** digitare un nome di query.  
  
    2.  Facoltativamente, digitare una descrizione per la query nella casella di testo **Descrizione** .  
  
    3.  Nella casella di riepilogo **Origine dati** selezionare l'origine dei dati su cui verrà eseguita la query denominata.  
  
    4.  Digitare la query nel riquadro inferiore oppure creare una query mediante gli strumenti grafici per la compilazione di query.  
  
    > [!NOTE]  
    >  L'interfaccia utente per la compilazione di query dipende dall'origine dei dati. Anziché un'interfaccia utente grafica, potrebbe venire visualizzata un'interfaccia utente generica, basata su testo. È possibile ottenere gli stessi risultati con interfacce utente diverse, ma è necessario eseguire procedure diverse. Per altre informazioni, vedere [Finestra di dialogo Crea query denominata o Modifica query denominata &#40;Analysis Services - Dati multidimensionali&#41;](../create-or-edit-named-query-dialog-box-analysis-services-multidimensional-data.md).  
  
5.  Fare clic su **OK**. Nell'intestazione di tabella verrà visualizzata un'icona con due tabelle sovrapposte, indicante che la tabella è stata sostituita da una query denominata.  
  
## <a name="see-also"></a>Vedere anche  
 [Viste origine dati in modelli multidimensionali](data-source-views-in-multidimensional-models.md)   
 [Definire calcoli denominati in una vista origine dati &#40;Analysis Services&#41;](define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
