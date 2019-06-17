---
title: Creare e gestire cataloghi full-text | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text search [SQL Server], using SQL Server Management Studio
ms.assetid: 824b7131-44a6-4815-89e6-62b7bab060e3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d90ba7f8e183beeeeefe25ea20834b07d7a1bf80
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011466"
---
# <a name="create-and-manage-full-text-catalogs"></a>Creazione e gestione dei cataloghi full-text
  Un catalogo full-text è un oggetto virtuale che non appartiene ad alcun filegroup. Si tratta di un concetto logico che fa riferimento a un gruppo di indici full-text.  
  
##  <a name="creating"></a> Creazione di un catalogo Full-Text  
  
#### <a name="to-create-a-full-text-catalog"></a>Per creare un catalogo full-text  
  
1.  In Esplora oggetti espandere il server, quindi **Database**e infine il database in cui si vuole creare il catalogo full-text.  
  
2.  Espandere **Archivio**, quindi fare clic con il pulsante destro del mouse su **Cataloghi full-text**.  
  
3.  Selezionare **Nuovo catalogo full-text**.  
  
4.  Nella finestra di dialogo **Nuovo catalogo full-text** specificare le informazioni per il catalogo da creare. Per altre informazioni, vedere [Nuovo catalogo full-text &#40;pagina Generale&#41;](../../integration-services/general-page-of-integration-services-designers-options.md).  
  
    > [!NOTE]  
    >  Gli ID dei cataloghi full-text iniziano da 00005 e vengono incrementati di un'unità per ogni catalogo creato.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
  
##  <a name="props"></a> Visualizzare le proprietà di un catalogo Full-Text  
 Per ottenere il valore di varie proprietà di indicizzazione full-text, è possibile utilizzare funzioni quali [!INCLUDE[tsql](../../includes/tsql-md.md)] FULLTEXTCATALOGPROPERTY. Queste informazioni sono utili per l'amministrazione e la risoluzione dei problemi relativi alla ricerca full-text.  
  
 Nella tabella seguente sono elencate le proprietà correlate ai cataloghi full-text.  
  
|Proprietà|Descrizione|Funzione|  
|--------------|-----------------|--------------|  
|`AccentSensitivity`|Impostazione relativa alla distinzione tra caratteri accentati e non accentati.|[FULLTEXTCATALOGPROPERTY](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)|  
|`ImportStatus`|Indica se il catalogo full-text viene importato o meno.|FULLTEXTCATALOGPROPERTY|  
|`IndexSize`|Dimensione del catalogo full-text in megabyte (MB).|FULLTEXTCATALOGPROPERTY|  
|`ItemCount`|Numero delle voci indicizzate incluse attualmente nel catalogo full-text.|FULLTEXTCATALOGPROPERTY|  
|`MergeStatus`|Indica se è in corso un'unione nell'indice master.|FULLTEXTCATALOGPROPERTY|  
|`PopulateCompletionAge`|Differenza espressa in secondi tra il completamento dell'ultimo popolamento di indici full-text e la data 01/01/1990 00:00:00.|FULLTEXTCATALOGPROPERTY|  
|`PopulateStatus`|Stato popolamento.<br /><br /> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|FULLTEXTCATALOGPROPERTY|  
|`UniqueKeyCount`|Numero di chiavi univoche nel catalogo full-text.|FULLTEXTCATALOGPROPERTY|  
  
  
  
##  <a name="rebuildone"></a> La ricompilazione di un catalogo Full-Text  
  
#### <a name="to-rebuild-a-full-text-catalog"></a>Per ricompilare un catalogo full-text  
  
1.  In Esplora oggetti espandere il server, quindi **Database**e infine il database contenente il catalogo full-text che si vuole ricompilare.  
  
2.  Espandere **Archivio**e quindi **Cataloghi full-text**.  
  
3.  Fare clic con il pulsante destro sul nome del catalogo full-text da ricompilare e scegliere **Ricompila**.  
  
4.  Quando viene visualizzato il messaggio **Eliminare il catalogo full-text e ricompilarlo?** , fare clic su **OK**.  
  
5.  Nella finestra di dialogo **Ricompila catalogo full-text** fare clic su **Chiudi**.  
  
  
  
##  <a name="rebuildall"></a> La ricompilazione di tutti i cataloghi Full-Text per un Database  
  
#### <a name="to-rebuild-the-full-text-catalogs-for-a-database"></a>Per ricompilare i cataloghi full-text di un database  
  
1.  In Esplora oggetti espandere il server, quindi **Database**e infine il database contenente i cataloghi full-text da ricompilare.  
  
2.  Espandere **Archivio**, quindi fare clic con il pulsante destro del mouse su **Cataloghi full-text**.  
  
3.  Scegliere **Ricompila tutto**.  
  
4.  Quando viene visualizzato il messaggio **Eliminare tutti i cataloghi full-text e ricompilarli?** , fare clic su **OK**.  
  
5.  Nella finestra di dialogo **Ricompila tutti i cataloghi full-text** scegliere **Chiudi**.  
  
  
  
##  <a name="removing"></a> Rimozione di un catalogo Full-Text da un Database  
  
#### <a name="to-remove-a-full-text-catalog-from-a-database"></a>Per rimuovere un catalogo full-text da un database  
  
1.  In Esplora oggetti espandere il server, quindi **Database**e infine il database contenente il catalogo full-text che si vuole rimuovere.  
  
2.  Espandere **Archivio**e quindi **Cataloghi full-text**.  
  
3.  Fare clic con il pulsante destro del mouse sul catalogo full-text da rimuovere e quindi scegliere **Elimina**.  
  
4.  Nella finestra di dialogo **Elimina oggetti** fare clic su **OK**.  
  
  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)  
  
  
