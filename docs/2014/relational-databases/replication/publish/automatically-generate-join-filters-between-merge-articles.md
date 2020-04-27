---
title: Generare automaticamente un set di filtri di join tra gli articoli di merge (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- automatic join filter generation
- join filters
ms.assetid: 7ef419f4-c17f-42a5-9068-174a3ec08941
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66c32615b3fd9f417eab27f156b2645c2c89593b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63020979"
---
# <a name="automatically-generate-a-set-of-join-filters-between-merge-articles-sql-server-management-studio"></a>Generazione automatica di un set di filtri di join tra gli articoli di merge (SQL Server Management Studio)
  Generare automaticamente un set di filtri di join nella pagina **Filtro righe tabella** della Creazione guidata nuova pubblicazione o nella pagina **Filtra righe** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>**. Per altre informazioni sull'uso della creazione guidata e l'accesso alla finestra di dialogo, vedere [Creare una pubblicazione](create-a-publication.md) e [Visualizzare e modificare le proprietà della pubblicazione](view-and-modify-publication-properties.md).  
  
> [!NOTE]  
>  Se si genera automaticamente un set di filtri di join nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** in seguito all'inizializzazione delle sottoscrizioni della pubblicazione, sarà necessario generare un nuovo snapshot e reinizializzare tutte le sottoscrizioni dopo aver apportato le modifiche. Per altre informazioni sui requisiti per la modifica delle proprietà, vedere [Modificare le proprietà di pubblicazioni e articoli](change-publication-and-article-properties.md).  
  
 È possibile creare manualmente i filtri join per un set di tabelle o generarli automaticamente durante la replica in base alle relazioni definite nelle tabelle tra la chiave esterna e la chiave primaria. Per altre informazioni sulla creazione manuale di filtri di join, vedere [Definire e modificare un filtro di join tra articoli di merge](define-and-modify-a-join-filter-between-merge-articles.md).  
  
### <a name="to-automatically-generate-a-set-of-join-filters-between-merge-articles"></a>Per generare automaticamente un set di filtri join tra articoli di merge  
  
1.  Nella pagina **Filtro righe tabella** della Creazione guidata nuova pubblicazione o nella pagina **Filtra righe** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** fare clic su **Aggiungi**, quindi su **Genera filtri automaticamente**.  
  
    > [!NOTE]  
    >  La generazione automatica dei filtri comporta l'eliminazione dei filtri di riga o dei filtri join esistenti nella pubblicazione. È possibile aggiungere filtri dopo averne generato automaticamente un set.  
  
2.  Per creare un filtro di riga seguire la procedura della finestra di dialogo **Genera filtri** . Il filtro di riga viene quindi esteso alle tabelle relative alla tabella filtrata mediante le relazioni tra chiave primaria e chiave esterna.  
  
    1.  Selezionare una tabella da filtrare dall'elenco a discesa.  
  
    2.  Creare un'istruzione di filtro nella casella di testo **Istruzione per il filtro** . È possibile digitare direttamente nell'area di testo nonché trascinare colonne dalla casella di riepilogo **Colonne** .  
  
         L'area di testo **Istruzione per il filtro** contiene il testo predefinito, nel formato seguente:  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
         Non è possibile modificare il testo predefinito. Digitare la clausola di filtro per un filtro di riga statico o per un filtro di riga con parametri dopo la parola chiave WHERE utilizzando la sintassi SQL standard. La clausola di filtro completa per un filtro di riga con parametri è simile alla seguente:  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         Per la clausola WHERE è consigliabile usare nomi in due parti. I nomi in tre e quattro parti non sono supportati.  
  
    3.  Specificare le opzioni di filtro.  
  
         Selezionare l'opzione corrispondente alla modalità di condivisione dei dati tra i Sottoscrittori, ovvero **Una riga di questa tabella verrà inviata a più sottoscrizioni** o **Una riga di questa tabella verrà inviata a una sola sottoscrizione**. Selezionando **Una riga di questa tabella verrà inviata a una sola sottoscrizione**è possibile ottimizzare le prestazioni della replica di tipo merge archiviando ed elaborando una minore quantità di metadati. È tuttavia necessario garantire che i dati vengano partizionati in modo da non consentire la replica di una riga in più Sottoscrittori. Per altre informazioni, vedere la sezione relativa all'impostazione delle opzioni delle partizioni nell'argomento [Filtri di riga con parametri](../merge/parameterized-filters-parameterized-row-filters.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     Il filtro specificato viene analizzato ed eseguito sulla tabella nella clausola SELECT. Se nell'istruzione di filtro sono presenti errori di sintassi o di altro tipo, verrà visualizzato un apposito messaggio di notifica e sarà possibile modificare l'istruzione.  
  
     Al termine dell'analisi dell'istruzione, i filtri join necessari vengono creati e visualizzati dalla replica nel riquadro **Tabelle filtrate** della pagina **Filtro righe tabella** o **Filtra righe** . Se i filtri vengono generati mediante la Creazione guidata nuova pubblicazione e non è stato ancora configurato il server di distribuzione per il server di pubblicazione sul quale viene eseguita questa procedura guidata, verrà richiesto di procedere a tale configurazione.  
  
4.  Se è visualizzata la finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** fare clic su **OK** per salvare e chiudere la finestra di dialogo.  
  
### <a name="to-modify-a-filter-that-was-automatically-generated"></a>Per modificare un filtro generato automaticamente  
  
1.  Nella pagina **Filtro righe tabella** della Creazione guidata nuova pubblicazione o nella pagina **Filtro righe** di **Proprietà pubblicazione - \<Pubblicazione>** selezionare un filtro nel riquadro **Tabelle filtrate** e quindi fare clic su **Modifica**.  
  
2.  Nella finestra di dialogo **Modifica filtro** o **Modifica join** modificare il filtro.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-filter-that-was-automatically-generated"></a>Per eliminare un filtro generato automaticamente  
  
1.  Nella pagina **Filtro righe tabella** della Creazione guidata nuova pubblicazione o nella pagina **Filtro righe** di **Proprietà pubblicazione - \<Pubblicazione>** selezionare un filtro nel riquadro **Tabelle filtrate** e quindi fare clic su **Elimina**.  
  
## <a name="see-also"></a>Vedi anche  
 [Filtri join](../merge/join-filters.md)   
 [Filtri di riga con parametri](../merge/parameterized-filters-parameterized-row-filters.md)  
  
  
