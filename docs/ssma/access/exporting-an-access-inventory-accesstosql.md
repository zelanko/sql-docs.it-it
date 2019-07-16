---
title: Esportazione di un inventario di Access (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, exporting metadata
- exporting
- exporting Access metadata
- exporting, Access metadata
- exporting, querying exported metadata
- inventories of Access databases
- querying exported metadata
ms.assetid: 7e1941fb-3d14-4265-aff6-c77a4026d0ed
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0c05eafd1fb58b6ece15f5ad8721228d9d4beab6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006561"
---
# <a name="exporting-an-access-inventory-accesstosql"></a>Esportazione di un inventario di Access (AccessToSQL)
Se si dispone di più database di Access e non si sono certi che quelli per eseguire la migrazione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile esportare un inventario di tutti i database di Access in un progetto. È quindi possibile esaminare e ottenere i metadati di inventario per determinare quali database e gli oggetti presenti in tali database per eseguire la migrazione. L'inventario è possibile rapidamente trovare le risposte alle domande, ad esempio il seguente:  
  
-   Quali sono i database più grandi?  
  
-   Chi possiede la maggior parte dei database?  
  
-   I database che contengono le stesse tabelle?  
  
-   I database che non sono stati modificati negli ultimi sei mesi?  
  
-   I database che contengono informazioni riservate?  
  
Alla fine di questo argomento vengono forniti esempi di query che consentono di rispondere a queste domande.  
  
## <a name="exported-metadata"></a>Metadati esportati  
SSMA consente di esportare i metadati relativi a accesso database, tabelle, colonne, indici, chiavi esterne, le query, report, form, macro e i moduli. I metadati relativi a ognuna di queste categorie di elementi vengono esportati in una tabella separata. Per gli schemi di queste tabelle, vedere [schemi di inventario di Access](access-inventory-schemas-accesstosql.md).  
  
## <a name="exporting-inventory-data"></a>Esportazione dei dati di inventario  
Per esportare un inventario di Access, è necessario prima di tutto aprire o creare un progetto SSMA e quindi aggiungere il database di Access che si desidera analizzare. Dopo aver aggiunto i database a un progetto SSMA, è esportare i metadati relativi a tali database per un determinato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database e nello schema. Se necessario, SSMA consente di creare tabelle per archiviare i metadati. SSMA aggiunge quindi i metadati sui database di Access per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
> [!NOTE]  
> Un database di Access può essere suddivisa in più file: un database back-end che contiene le tabelle e i database front-end contenenti query, form, i report, le macro, moduli e tasti di scelta rapida. Se si vuole eseguire la migrazione di un database di split a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aggiungere i database front-end in SSMA.  
  
Le istruzioni seguenti descrivono come creare un progetto, aggiungere database al progetto, connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e quindi esportare i dati di inventario.  
  
**Per creare un progetto**  
  
1.  Aprire SSMA per l'accesso.  
  
2.  Nel menu **File** selezionare **Nuovo progetto**.  
  
    Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
3.  Nel **nome** immettere un nome per il progetto.  
  
4.  Nel **posizione** casella, immettere o selezionare una cartella per il progetto.  
  
5.  Nel **eseguire la migrazione a** combinata, selezionare la versione di destinazione a cui si desidera eseguire la migrazione e quindi fare clic su **OK**.  
  
Per altre informazioni sulla creazione di progetti, vedere [creazione e gestione di progetti](creating-and-managing-projects-accesstosql.md).  
  
**Per trovare e aggiungere i database**  
  
1.  Nel **File** menu, fare clic su **trovare database**.  
  
2.  In Creazione guidata database di ricerca, immettere l'unità, percorso del file o percorso UNC che si desidera cercare. In alternativa, fare clic su **esplorare** per selezionare l'unità o cartella di rete.  
  
3.  Fare clic su **Add** per aggiungere il percorso nella casella di riepilogo.  
  
    Ripetere i due passaggi precedenti per aggiungere percorsi di ricerca aggiuntive.  
  
4.  Facoltativamente, aggiungere criteri di ricerca per restringere l'elenco di database che vengono restituiti.  
  
    > [!IMPORTANT]  
    > Il **tutto o parte del nome del file** casella di testo non supporta caratteri jolly.  
  
5.  Fare clic su **Scan**.  
  
    Viene visualizzata la pagina di analisi. Vengono visualizzati i database che sono stati trovati e lo stato di avanzamento di ricerca. Per arrestare la ricerca, fare clic su **arrestare**.  
  
6.  Nella pagina Seleziona file, selezionare ogni database che si desidera aggiungere al progetto.  
  
    È possibile usare la **Seleziona tutto** e **Clear All** pulsanti nella parte superiore dell'elenco per selezionare o deselezionare tutti i database. È anche possibile tenere premuto il tasto CTRL per selezionare più righe o tenere premuto il tasto MAIUSC basso per selezionare un intervallo di righe.  
  
7.  Fare clic su **Avanti**.  
  
8.  Nella pagina di verifica, fare clic su **fine**.  
  
Per altre informazioni sull'aggiunta di database per i progetti, vedere [aggiunta e rimozione di file di Database di Access](adding-and-removing-access-database-files-accesstosql.md).  
  
**Per connettersi a SQL Server**  
  
1.  Nel **File** dal menu **Connetti al Server SQL**.  
  
2.  Nella finestra di dialogo di connessione, immettere o selezionare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Se ci si connette all'istanza predefinita nel computer locale, è possibile immettere **localhost** o un punto ( **.** ).  
  
    -   Se ci si connette all'istanza predefinita in un altro computer, immettere il nome del computer.  
  
    -   Se ci si connette a un'istanza denominata, immettere il nome del computer, una barra rovesciata e il nome dell'istanza. Ad esempio: MyServer\MyInstance.  
  
3.  Nel **Database** immettere il nome del database di destinazione per i metadati esportati.  
  
4.  Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è configurato per accettare le connessioni su una porta non predefinito, immettere il numero di porta usato per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] connessioni nel **porta Server** casella. Per l'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il numero di porta predefinito è 1433. Per le istanze denominate, SSMA tenta di ottenere il numero di porta dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio Browser.  
  
5.  Nel **autenticazione** -menu a discesa, seleziona il tipo di autenticazione da usare per la connessione. Per usare l'account di Windows corrente, selezionare **Windows autenticazione**. Usare un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso, selezionare **autenticazione di SQL Server**e quindi specificare un nome utente e password.  
  
Per altre informazioni sulla connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [ci si connette a SQL Server &#40;AccessToSQL&#41;](../../ssma/access/connecting-to-sql-server-accesstosql.md).  
  
**Per esportare le informazioni di inventario**  
  
1.  Nel Visualizzatore metadati di accesso, espandere **accesso metabase**.  
  
2.  Selezionare la casella di controllo accanto a **database**.  
  
    Per omettere i singoli database o oggetti di database, espandere la **database** cartella e quindi deselezionare la casella di controllo accanto al database o un oggetto di database.  
  
3.  Fare doppio clic su **database** e selezionare **esportare Schema**.  
  
4.  Nel **selezionare uno Schema per l'esportazione** finestra di dialogo, selezionare lo schema di destinazione per i metadati esportati e quindi fare clic su **OK**.  
  
Ogni volta che si esporta i metadati, SSMA accoda i dati per l'inventario. I dati esistenti nell'inventario non viene aggiornati o eliminati.  
  
## <a name="querying-the-exported-metadata"></a>L'esecuzione di query i metadati esportati  
Dopo avere esportato i metadati relativi a database di Access, è possibile eseguire una query dei metadati. Le istruzioni seguenti viene descritto come per utilizzare la finestra dell'Editor di Query in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per eseguire query.  
  
**Eseguire query sui metadati**  
  
1.  Dal **avviare** dal menu **tutti i programmi**, scegliere **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005** oppure a **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008**o a **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012**, quindi fare clic su **SQL Server Management Studio**.  
  
2.  Nel **Connetti al Server** finestra di dialogo, verificare le impostazioni e quindi fare clic su **Connect**.  
  
3.  Sulla barra degli strumenti Management Studio, fare clic su **nuova Query** per aprire l'Editor di Query.  
  
4.  Nella finestra dell'Editor di Query, immettere una query. Nella sezione seguente vengono illustrati alcuni esempi.  
  
5.  Premere il tasto F5 per eseguire la query.  
  
## <a name="query-examples"></a>Esempi di query  
Prima di eseguire una delle query seguenti, è consigliabile eseguire un uso *database_name* query per assicurarsi che le query vengono eseguite sul database che contiene i metadati esportati. Ad esempio, se in un database denominato MyAccessMetadata esportato i metadati, aggiungere quanto segue all'inizio del [!INCLUDE[tsql](../../includes/tsql-md.md)] codice:  
  
```  
USE MyAccessMetadata;  
GO  
```  
Tutti gli esempi seguenti usano il **dbo** dello schema. Se si esportato i metadati in un altro schema, assicurarsi di modificare lo schema quando si eseguono tali query.  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>Quali tabelle e colonne si trovano in questi database?  
La query seguente unisce le tabelle che contengono colonne, tabelle e i metadati del database e quindi restituisce i nomi di tutti i database, tabelle e colonne, ordinati in base al nome di colonna:  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D.DatabaseId  
ORDER BY ColumnName;  
```  
  
### <a name="what-are-the-largest-databases"></a>Quali sono i database più grandi?  
La query seguente restituisce il nome del database, dimensioni del file e numero di tabelle in ogni database di Access, ordinati per dimensioni file:  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>Chi è il proprietario della maggior parte dei database?  
La query seguente restituisce il nome del database e il proprietario di ogni database di Access, ordinati dal proprietario.  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>I database che contengono le stesse tabelle?  
La query seguente viene utilizzata una sottoquery per trovare tutti i nomi delle tabelle che vengono visualizzati più volte nell'elenco di tabelle e quindi Usa questo elenco di tabelle per ottenere il nome del database. I risultati vengono restituiti come il nome del database e quindi il nome della tabella e sono ordinati in base al nome di tabella.  
  
```  
SELECT DatabaseName, TableName   
FROM dbo.SSMA_Access_InventoryTables T  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON D.DatabaseId = T.DatabaseId  
WHERE TableName IN (  
SELECT TableName   
FROM dbo.SSMA_Access_InventoryTables  
GROUP BY TableName   
HAVING count(*)>1  
)  
ORDER BY TableName;  
```  
  
### <a name="which-databases-were-not-modified-in-the-last-six-months"></a>I database che non sono stati modificati negli ultimi sei mesi?  
La query seguente ottiene la data corrente, ottiene il valore del mese per sei mesi fa e quindi restituisce un elenco di database con una data di modifica maggiore di sei mesi fa.  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>I database che contengono informazioni riservate?  
I database di Access potrebbero contenere informazioni sensibili o personale. È possibile spostare questi database a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per sfruttare le funzionalità di sicurezza. Se si sa che hanno un nome specifico colonne contenenti dati sensibili o contengono caratteri specifici, è possibile usare una query per trovare tutte le colonne che contengono tali informazioni. Ad esempio, è possibile trovare tutte le colonne che includono la stringa "salary".  La query restituisce quindi il nome del database, nome della tabella e il nome di colonna.  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D. DatabaseId  
WHERE ColumnName LIKE '%salary%';  
```  
Se non si conosce il nome della colonna, è possibile scrivere una query per restituire tutte le colonne. A tale scopo, rimuovere la clausola WHERE dalla query precedente.  
  
## <a name="see-also"></a>Vedere anche  
[Preparazione dei database di Access per la migrazione](preparing-access-databases-for-migration-accesstosql.md)  
  
