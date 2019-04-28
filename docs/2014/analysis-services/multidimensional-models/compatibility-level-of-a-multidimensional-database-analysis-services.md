---
title: Impostare la compatibilità a livello di un Database multidimensionale (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 978279e6-a581-4184-af9d-8701b9826a89
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fcf32b558d34340d727a357136884b8d6530887b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62701070"
---
# <a name="set-the-compatibility-level-of-a-multidimensional-database-analysis-services"></a>Impostare il livello di compatibilità di un database multidimensionale (Analysis Services)
  In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]la proprietà del livello di compatibilità del database determina il livello funzionale di un database. I livelli di compatibilità sono univoci per ogni tipo di modello. Ad esempio, un livello di compatibilità di `1100` ha un significato diverso a seconda del fatto che il database è multidimensionale o tabulare.  
  
 In questo argomento viene descritto il livello di compatibilità solo per i database multidimensionali. Per altre informazioni sulle soluzioni tabulari, vedere [livello di compatibilità &#40;SP1 in formato tabulare SSAS&#41;](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).  
  
> [!NOTE]  
>  I modelli tabulari presentano livelli di compatibilità dei database aggiuntivi non applicabili ai modelli multidimensionali. Il livello di compatibilità `1103` non esiste per i modelli multidimensionali. Visualizzare [quali sono le novità per il modello tabulare in SQL Server 2012 SP1 e livello di compatibilità](https://go.microsoft.com/fwlink/?LinkId=301727) per altre informazioni sulle `1103` per le soluzioni tabulari.  
  
 **Livelli di compatibilità per database multidimensionali**  
  
 Attualmente, l'unico comportamento di database multidimensionale che varia in base al livello funzionale è l'architettura di archiviazione basata su stringa. L'aumento del livello di compatibilità di un database consente di ignorare il limite massimo di 4 GB per l'archiviazione di stringhe di misure e dimensioni.  
  
 Per un database multidimensionale, tra i valori validi per la proprietà `CompatibilityLevel` sono inclusi i seguenti:  
  
|Impostazione|Descrizione|  
|-------------|-----------------|  
|`1050`|Questo valore non è visibile negli script o negli strumenti, ma corrisponde ai database creati in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. Qualsiasi database il cui `CompatibilityLevel` non è impostato in modo esplicito viene eseguito in modo implicito al livello `1050`.|  
|`1100`|Si tratta del valore predefinito per i nuovi database creati in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Questa impostazione può essere specificata anche per i database creati in versioni precedenti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per consentire l'utilizzo di funzionalità che sono supportate solo a questo livello di compatibilità (vale a dire, archivio di stringhe esteso per misure Distinct Count o attributi della dimensione contenenti dati di tipo stringa).<br /><br /> I database con un `CompatibilityLevel` impostata su `1100` ottengono una proprietà aggiuntiva, `StringStoresCompatibilityLevel`, che consente di scegliere archiviazione alternativa di stringhe per partizioni e dimensioni.|  
  
> [!WARNING]  
>  L'impostazione della compatibilità del database su un livello superiore è irreversibile. Dopo aver aumentato il livello di compatibilità su `1100`, è necessario continuare a eseguire il database in server più recenti. Non è possibile eseguire il rollback al `1050`. È possibile collegare o ripristinare un' `1100` database in una versione server precedente a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="prerequisites"></a>Prerequisiti  
 I livelli di compatibilità del database vengono introdotti in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Per visualizzare o impostare il livello di compatibilità del database, è necessario [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o versione successiva.  
  
 Il database non può essere un cubo locale. I cubi locali non supportano la proprietà `CompatibilityLevel`.  
  
 Il database deve essere stato creato in una versione precedente (SQL Server 2008 R2 o versioni precedenti), quindi collegato o ripristinato a un server [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o versione successiva. I database distribuiti in SQL Server 2012 sono già al livello `1100` e non è possibile effettuare il downgrade per l'esecuzione a un livello inferiore.  
  
## <a name="determine-the-existing-database-compatibility-level-for-a-multidimensional-database"></a>Determinare il livello di compatibilità del database esistente per un database multidimensionale  
 L'unico modo per visualizzare o modificare il livello di compatibilità del database è tramite XMLA. È possibile visualizzare o modificare lo script XMLA che specifica il database in SQL Server Management Studio.  
  
 Se si cerca la definizione XMLA di un database per la proprietà `CompatibilityLevel` e non esiste, è probabile che il database sia eseguito al livello di compatibilità `1050`.  
  
 Le istruzioni per la visualizzazione e la modifica dello script XMLA vengono fornite nella sezione successiva.  
  
## <a name="set-the-database-compatibility-level-in-sql-server-management-studio"></a>Impostare il livello di compatibilità del database in SQL Server Management Studio  
  
1.  Prima di aumentare il livello di compatibilità, eseguire il backup del database nel caso si desideri annullare le modifiche in un momento successivo.  
  
2.  Usando SQL Server Management Studio connettersi al server [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cui è ospitato il database.  
  
3.  Fare clic con il pulsante destro del mouse sul nome del database, scegliere **Crea script per database**, scegliere **Genera codice per istruzione ALTER in**, quindi selezionare **Nuova finestra editor di query**. Una rappresentazione XMLA del database verrà visualizzata in una nuova finestra.  
  
4.  Copiare l'elemento XML seguente:  
  
    ```  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    ```  
  
5.  Incollarlo dopo l'elemento di chiusura `</Annotations>` e prima dell'elemento `<Language>` . Il codice XML dovrebbe essere simile a quello riportato nell'esempio seguente:  
  
    ```  
    </Annotations>  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    <Language>1033</Language>  
    ```  
  
6.  Salvare il file.  
  
7.  Per eseguire lo script, scegliere **Esegui** dal menu Query o premere F5.  
  
## <a name="supported-operations-that-require-the-same-compatibility-level"></a>Operazioni supportate per le quali è richiesto lo stesso livello di compatibilità  
 Per le operazioni indicate di seguito è necessario che il livello di compatibilità dei database di origine sia lo stesso.  
  
1.  L'unione di partizioni da database diversi è supportata solo se entrambi i database condividono lo stesso livello di compatibilità.  
  
2.  Per utilizzare dimensioni collegate da un altro database, è necessario lo stesso livello di compatibilità. Ad esempio, se si desidera utilizzare una dimensione collegata da un [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] del database in un [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] database, è necessario trasferire il [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] del database a un [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] server e impostare la compatibilità con il livello su `1100`.  
  
3.  La sincronizzazione di server è supportata solo per server in cui viene condivisa la stessa versione e lo stesso livello di compatibilità del database.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Dopo aver aumentato il livello di compatibilità del database, è possibile impostare la proprietà `StringStoresCompatibilityLevel` in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. In questo modo viene aumentato l'archivio di stringhe per misure e dimensioni. Per altre informazioni su questa funzionalità, vedere [Configurare l'archivio di stringhe per dimensioni e partizioni](configure-string-storage-for-dimensions-and-partitions.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Backup, ripristino e sincronizzazione di database &#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
