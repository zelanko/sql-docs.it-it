---
title: Passare un database di Analysis Services tra le modalità ReadOnly e ReadWrite | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e1ae8fc032a1f728372e9b4e764281ea8df8ddaa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63020055"
---
# <a name="switch-an-analysis-services-database-between-readonly-and-readwrite-modes"></a>Passare un database di Analysis Services tra le modalità ReadOnly e ReadWrite
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Gli amministratori del database possono cambiare la modalità di lettura/scrittura di un database tabulare o multidimensionale nell'ambito di un'operazione di più ampio respiro per la distribuzione di un carico di lavoro di query tra più server usati solo per le query.  
  
 In un database è possibile passare da una modalità all'altra in vari modi. In questo documento vengono illustrati gli scenari comuni seguenti:  
  
-   In modo interattivo tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   A livello di programmazione tramite AMO  
  
-   Tramite script usando XMLA o TMSL  
  
## <a name="switch-the-readwrite-mode-of-a-database-interactively-using-management-studio"></a>Attivare la modalità lettura/scrittura di un database in modo interattivo tramite Management Studio  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse sul database, quindi scegliere **Proprietà**.  
  
     Prendere nota del percorso. Un percorso di archiviazione del database vuoto indica che la cartella del database si trova nella cartella di dati del server.  
  
2.  Il database e scegliere **Scollega...**  
  
3.  Assegnare una password al database da scollegare, quindi fare clic su **OK** per eseguire il comando.  
  
4.  In Esplora oggetti fare doppio clic il **database** cartella e selezionare **Connetti...**  
  
5.  Nella casella di testo **cartella** digitare il percorso originale della cartella del database. In alternativa, è possibile usare il pulsante Sfoglia (**...** ) per individuare la cartella di database.  
  
6.  Selezionare la modalità di lettura/scrittura per il database.  
  
7.  Digitare la password e fare clic su **OK** per eseguire il comando di collegamento.  
  
## <a name="switch-the-readwrite-mode-to-a-database-programmatically-using-amo"></a>Attivare la modalità lettura/scrittura di un database a livello di programmazione tramite AMO  
 Nell'applicazione C# richiamare `SwitchReadWrite()` con i parametri necessari. Compilare ed eseguire il codice per spostare il database.  
  
```  
private void SwitchReadWrite(Server server, string dbName, ReadWriteMode dbReadWriteMode)  
{  
    if (server.Databases.ContainsName(dbName))  
    {  
        Database db;  
        string databaseLocation;  
        db = server.Databases[dbName];  
        databaseLocation = db.DbStorageLocation;  
  
              if (databaseLocation == null)  
            {  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
  
    String[] possibleFolders = Directory.GetDirectories(dataDir, string.Concat(dbName,"*"), SearchOption.TopDirectoryOnly);  
  
   if (possibleFolders.Length > 1)  
         {  
         List<String> sortedFolders = new List<string>(possibleFolders.Length);  
         sortedFolders.AddRange(possibleFolders);  
         sortedFolders.Sort();  
         databaseLocation = sortedFolders[sortedFolders.Count - 1];  
         }  
         else  
         {  
         databaseLocation = possibleFolders[0];  
          }  
        }  
    db.Detach();  
    server.Attach(databaseLocation, dbReadWriteMode);  
    }  
}  
  
```  
  
## <a name="switch-the-readwrite-mode-to-a-database-by-script-using-xmla"></a>Attivare la modalità lettura/scrittura di un database tramite script usando XMLA  
 Le istruzioni seguenti si applicano a database multidimensionali e tabulari in modalità di compatibilità 1050, 1100 o 1103.  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse sul database, quindi scegliere **Proprietà**.  
  
     Prendere nota del percorso. Un percorso di archiviazione del database vuoto indica che la cartella del database si trova nella cartella di dati del server.  
  
2.  Il database e scegliere **Scollega...**  
  
3.  Aprire una nuova scheda XMLA in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
4.  Copiare il modello di script seguente per XMLA:  
  
    ```  
    <Detach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
       <Object>  
          <DatabaseID>%dbName%</DatabaseID>  
          <Password>%password%</Password>  
       </Object>  
    </Detach>  
    ```  
  
5.  Sostituire `%dbName%` con il nome del database e `%password%` con la password. I caratteri % fanno parte del modello e devono essere rimossi.  
  
6.  Eseguire il comando XMLA.  
  
7.  Copiare il modello di script seguente per XMLA in una nuova scheda XMLA:  
  
    ```  
    <Attach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
       <Folder>%dbFolder%</Folder>  
       <ReadWriteMode xmlns="http://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>  
    </Attach>  
    ```  
  
8.  Sostituire `%dbFolder%` con il percorso completo in formato UNC della cartella del database, `%ReadOnlyMode%` con il valore **ReadOnly** o **ReadWrite**corrispondente e `%password%` con la password. I caratteri % fanno parte del modello e devono essere rimossi.  
  
9. Eseguire il comando XMLA.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Disponibilità elevata e scalabilità in Analysis Services](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)   
 [Collegamento e scollegamento di database di Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Percorso di archiviazione dei database](../../analysis-services/multidimensional-models/database-storage-location.md)   
 [Proprietà ReadWriteMode del database](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Elemento Attach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Elemento Detach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [Elemento ReadWriteMode](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/readwritemode-element)   
 [Elemento DbStorageLocation](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)  
  
  
