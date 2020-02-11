---
title: Definizione di un'origine dati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5a3e83c9-8788-431e-85b0-a68c79377ff3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a9b2b248207d19f99aae3b07837d624fb9bb9cf6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079343"
---
# <a name="defining-a-data-source"></a>Definizione di un'origine dei dati
  Dopo aver creato un progetto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , la prima operazione consiste nel definire una o più origini dati da usare. Quando si definisce un'origine dei dati si specificano le informazioni sulla stringa di connessione che verrà utilizzata per connettersi all'origine dei dati. Per altre informazioni, vedere [Creare un'origine dati &#40;SSAS multidimensionale&#41;](multidimensional-models/create-a-data-source-ssas-multidimensional.md).  
  
 Nell'attività seguente il database di esempio AdventureWorksDWSQLServer2012 verrà definito come origine dati del progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial. Ai fini di questa esercitazione questo database si trova nel computer locale. Tuttavia, i database di origine sono spesso ospitati in uno o più computer remoti.  
  
### <a name="to-define-a-new-data-source"></a>Per definire una nuova origine dati  
  
1.  In Esplora soluzioni (a destra della finestra di Microsoft Visual Studio) fare clic con il pulsante destro del mouse su **Origini dati**, quindi scegliere **Nuova origine dati**.  
  
2.  Nella pagina **creazione guidata origine dati** della **creazione guidata origine dati**fare clic su **Avanti** per aprire la pagina **selezionare la modalità di definizione della connessione** .  
  
3.  Nella pagina **Selezione metodo di definizione connessione** è possibile definire un'origine dati basata su una nuova connessione, su una connessione esistente o su un oggetto origine dati definito in precedenza. In questa esercitazione verranno illustrate le procedure per definire un'origine dati basata su una nuova connessione. Verificare che l'opzione **Crea un'origine dati basata su una connessione nuova o esistente** sia selezionata e fare clic su **Nuova**.  
  
4.  Nella finestra di dialogo **Gestione connessione** si definiscono le proprietà di connessione per l'origine dati. Nella casella di riepilogo **Provider** verificare che l'opzione **OLE DB nativo\SQL Server Native Client 11.0** sia selezionata.  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]supporta anche altri provider, che vengono visualizzati nell'elenco **provider** .  
  
5.  Nella casella di testo **nome server** Digitare `localhost`.  
  
     Per connettersi a un'istanza denominata nel computer locale, digitare **localhost\\<nome\>istanza**. Per connettersi al computer specifico anziché al computer locale, digitare il nome o l'indirizzo IP del computer.  
  
6.  Verificare che l'opzione **Usa autenticazione di Windows** sia selezionata. Nell'elenco **Selezionare o immettere un nome di database** selezionare **AdventureWorksDW2012**.  
  
7.  Fare clic su **Test connessione** per testare la connessione al database.  
  
8.  Fare clic su **OK** e quindi su **Avanti**.  
  
9. Nella pagina **Impostazioni di rappresentazione** della procedura guidata si definiscono le credenziali di sicurezza per [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] necessarie per connettersi all'origine dati. La rappresentazione influisce sull'account di Windows utilizzato per connettersi all'origine dati quando è selezionata l'autenticazione di Windows. 
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] non supporta la rappresentazione per l'elaborazione di oggetti OLAP. Selezionare **Usa account del servizio**e quindi fare clic su **Avanti**.  
  
10. Nella pagina **Completamento procedura guidata** accettare il nome predefinito **Adventure Works DW 2012**e fare clic su **Fine** per creare la nuova origine dati.  
  
> [!NOTE]  
>  Per modificare le proprietà dell'origine dati dopo che è stata creata, fare doppio clic su di essa nella cartella **Origini dati** per visualizzarne le proprietà in **Progettazione origine dati**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Definizione di una vista origine dati](lesson-1-3-defining-a-data-source-view.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un'origine dati &#40;SSAS multidimensionale&#41;](multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
  
