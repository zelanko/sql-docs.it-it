---
title: Passare un database di Analysis Services tra le modalità ReadOnly e ReadWrite | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ReadOnly property
- ReadWriteMode command
- operations [Analysis Services - multidimensional data]
ms.assetid: 4eff8181-08dd-4fad-b091-d400fc21a020
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 48bb00cba9a01029da31146f9e98e2ef8b3627d6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62741363"
---
# <a name="switch-an-analysis-services-database-between-readonly-and-readwrite-modes"></a>Passare un database di Analysis Services tra le modalità ReadOnly e ReadWrite
  In alcune situazioni frequenti, un amministratore del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] potrebbe voler modificare la modalità lettura/scrittura di un database tabulare o multidimensionale. Queste situazioni spesso sono determinate da esigenze aziendali, ad esempio condividere il database fra un pool di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] server per migliorare l'esperienza utente.  
  
 In un database è possibile passare da una modalità all'altra in vari modi. In questo documento vengono illustrati gli scenari comuni seguenti:  
  
-   In modo interattivo tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   A livello di programmazione tramite AMO  
  
-   Tramite script utilizzando XMLA  
  
## <a name="procedures"></a>Procedure  
  
#### <a name="to-switch-the-readwrite-mode-of-a-database-interactively-using-management-studio"></a>Per attivare la modalità lettura/scrittura di un database in modo interattivo tramite Management Studio  
  
1.  Individuare il database di cui cambiare la modalità nel riquadro sinistro o destro di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Il database e scegliere **proprietà**. Individuare la cartella del database e prendere nota del percorso. Un percorso di archiviazione del database vuoto indica che la cartella del database si trova nella cartella di dati del server.  
  
    > [!IMPORTANT]  
    >  Non appena il database viene scollegato, [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] non consente più di ottenerne il percorso.  
  
3.  Il database e scegliere **Scollega...**  
  
4.  Assegnare una password al database da scollegare, quindi fare clic su **OK** per eseguire il comando.  
  
5.  Individuare il **database** cartella nel riquadro sinistro o destro di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
6.  Fare doppio clic il **database** cartella e selezionare **Connetti...**  
  
7.  Nella casella di testo **cartella** digitare il percorso originale della cartella del database. In alternativa, è possibile usare il pulsante Sfoglia (**...** ) per individuare la cartella di database.  
  
8.  Selezionare la modalità di lettura/scrittura per il database.  
  
9. Digitare la password usata nel passaggio 3 e fare clic su **OK** per eseguire il comando attach.  
  
#### <a name="to-switch-the-readwrite-mode-to-a-database-programmatically-using-amo"></a>Per attivare la modalità lettura/scrittura di un database a livello di programmazione tramite AMO  
  
1.  Nell'applicazione C# adattare il codice di esempio seguente e completare le attività indicate.  
  
 `private void SwitchReadWrite(Server server, string dbName,`  
  
 `ReadWriteMode dbReadWriteMode)`  
  
 `{`  
  
 `if (server.Databases.ContainsName(dbName))`  
  
 `{`  
  
 `Database db;`  
  
 `string databaseLocation;`  
  
 `db = server.Databases[dbName];`  
  
 `databaseLocation = db.DbStorageLocation;`  
  
 `if (databaseLocation == null)`  
  
 `{`  
  
 `string dataDir = server.ServerProperties["DataDir"].Value;`  
  
 `String[] possibleFolders = Directory.GetDirectories(dataDir, string.Concat(dbName,"*"), SearchOption.TopDirectoryOnly);`  
  
 `if (possibleFolders.Length > 1)`  
  
 `{`  
  
 `List<String> sortedFolders = new List<string>(possibleFolders.Length);`  
  
 `sortedFolders.AddRange(possibleFolders);`  
  
 `sortedFolders.Sort();`  
  
 `databaseLocation = sortedFolders[sortedFolders.Count - 1];`  
  
 `}`  
  
 `else`  
  
 `{`  
  
 `databaseLocation = possibleFolders[0];`  
  
 `}`  
  
 `}`  
  
 `db.Detach();`  
  
 `server.Attach(databaseLocation, dbReadWriteMode);`  
  
 `}`  
  
 `}`  
  
1.  Nell'applicazione C# richiamare `SwitchReadWrite()` con i parametri necessari.  
  
2.  Compilare ed eseguire il codice per spostare il database.  
  
#### <a name="to-switch-the-readwrite-mode-to-a-database-by-script-using-xmla"></a>Per attivare la modalità lettura/scrittura di un database tramite script utilizzando XMLA  
  
1.  Individuare il database di cui cambiare la modalità nel riquadro sinistro o destro di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Il database e scegliere **proprietà**. Individuare la cartella del database e prendere nota del percorso. Un percorso di archiviazione del database vuoto indica che la cartella del database si trova nella cartella di dati del server.  
  
    > [!IMPORTANT]  
    >  Non appena il database viene scollegato, [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] non consente più di ottenerne il percorso.  
  
3.  Aprire una nuova scheda XMLA in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
4.  Copiare il modello di script seguente per XMLA:  
  
 `<Detach xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Object>`  
  
 `<DatabaseID>%dbName%</DatabaseID>`  
  
 `<Password>%password%</Password>`  
  
 `</Object>`  
  
 `</Detach>`  
  
1.  Sostituire `%dbName%` con il nome del database e `%password%` con la password. I caratteri % fanno parte del modello e devono essere rimossi.  
  
2.  Eseguire il comando XMLA.  
  
3.  Copiare il modello di script seguente per XMLA in una nuova scheda XMLA:  
  
 `<Attach xmlns="https://schemas.microsoft.com/analysisservices/2003` `/engine` `">`  
  
 `<Folder>%dbFolder%</Folder>`  
  
 `<ReadWriteMode xmlns="https://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>`  
  
 `</Attach>`  
  
1.  Sostituire `%dbFolder%` con il percorso completo in formato UNC della cartella del database, `%ReadOnlyMode%` con il valore `ReadOnly` o `ReadWrite` corrispondente e `%password%` con la password. I caratteri % fanno parte del modello e devono essere rimossi.  
  
2.  Eseguire il comando XMLA.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Collegamento e scollegamento di database di Analysis Services](attach-and-detach-analysis-services-databases.md)   
 [Percorso di archiviazione dei database](database-storage-location.md)   
 [Proprietà ReadWriteMode del database](database-readwritemodes.md)   
 [Elemento Attach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Elemento Detach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [Elemento ReadWriteMode](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/readwritemode-element)   
 [Elemento DbStorageLocation](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)  
  
  
