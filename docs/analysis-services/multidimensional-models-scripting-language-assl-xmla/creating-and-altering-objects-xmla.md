---
title: Creazione e modifica di oggetti (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 86f52c2ea61b8b62ea9bfe5ffe6b3c7b06977740
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63231965"
---
# <a name="creating-and-altering-objects-xmla"></a>Creazione e modifica di oggetti (XMLA)
  Gli oggetti principali possono essere creati, modificati ed eliminati in modo indipendente. Di seguito vengono elencati gli oggetti principali:  
  
-   Server  
  
-   Database  
  
-   Dimensioni  
  
-   Cubi  
  
-   Gruppi di misure  
  
-   Partizioni  
  
-   prospettive  
  
-   Modelli di data mining  
  
-   Ruoli  
  
-   Comandi associati a un server o a un database  
  
-   Origini dei dati  
  
 Si utilizza il [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) comando per creare un oggetto principale in un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e la [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) comandi per modificare un oggetto principale esistente in un'istanza. Entrambi i comandi vengono eseguiti tramite il [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) (metodo).  
  
## <a name="creating-objects"></a>Creazione di oggetti  
 Quando si creano oggetti usando il **Create** metodo, è necessario innanzitutto identificare l'oggetto padre che contiene il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oggetto da creare. Identificare l'oggetto padre, che fornisce un riferimento all'oggetto nel [ParentObject](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) proprietà delle **crea** comando. Ogni riferimento all'oggetto contiene gli identificatori di oggetto necessari per identificare in modo univoco l'oggetto padre per il **Create** comando. Per altre informazioni sui riferimenti a oggetti, vedere [definizione e identificazione di oggetti &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md).  
  
 Si supponga ad esempio che sia necessario fornire un riferimento a un oggetto per un cubo per creare un nuovo gruppo di misure per il cubo stesso. Il riferimento all'oggetto per il cubo nel **ParentObject** proprietà contiene un identificatore del database sia un identificatore del cubo, come lo stesso identificatore di cubo potrebbe potenzialmente essere usato in un database diverso.  
  
 Il [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) elemento contiene elementi di Analysis Services Scripting Language (ASSL) che definiscono l'oggetto principale da creare. Per altre informazioni su ASSL, vedere [lo sviluppo con Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Se si imposta il **AllowOverwrite** attributo il **crea** comando su true, è possibile sovrascrivere un oggetto principale esistente con l'identificatore specificato. In caso contrario, se un oggetto principale con l'identificatore specificato esiste già nell'oggetto padre si verifica un errore.  
  
 Per altre informazioni sul **Create** comando, vedere [Crea elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla).  
  
### <a name="creating-session-objects"></a>Creazione di oggetti di sessione  
 Gli oggetti di sessione sono oggetti temporanei disponibili solo nella sessione esplicita o implicita utilizzata da un'applicazione client che vengono eliminati quando la sessione è terminata. È possibile creare oggetti di sessione impostando il **ambito** attributo del **Create** comando *sessione*.  
  
> [!NOTE]  
>  Quando si usa la *sessione* impostazione, il **ObjectDefinition** elemento può contenere solo [dimensione](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl), [cubo](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl), o [ Elemento MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) gli elementi ASSL.  
  
## <a name="altering-objects"></a>Modifica di oggetti  
 Quando si modificano gli oggetti utilizzando il **Alter** metodo, è necessario innanzitutto identificare l'oggetto da modificare, fornendo un riferimento all'oggetto nel [oggetto](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) proprietà del **Alter**comando. Ogni riferimento all'oggetto contiene gli identificatori di oggetto necessari per identificare in modo univoco l'oggetto per il **Alter** comando. Per altre informazioni sui riferimenti a oggetti, vedere [definizione e identificazione di oggetti &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md).  
  
 Si supponga ad esempio che sia necessario fornire un riferimento a un oggetto per un cubo per modificarne la struttura. Il riferimento all'oggetto per il cubo nel **oggetto** proprietà contiene un identificatore del database sia un identificatore del cubo, come lo stesso identificatore di cubo potrebbe potenzialmente essere usato in un database diverso.  
  
 Il **ObjectDefinition** elemento contiene elementi ASSL che definiscono l'oggetto principale da modificare. Per altre informazioni su ASSL, vedere [lo sviluppo con Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Se si imposta la **AllowCreate** attributo il **Alter** comando su true, è possibile creare l'oggetto principale specificato se l'oggetto non esiste. In caso contrario, se un oggetto principale specificato non esiste si verifica un errore.  
  
### <a name="using-the-objectexpansion-attribute"></a>Utilizzo dell'attributo ObjectExpansion  
 Se si siano modificando solo le proprietà dell'oggetto principale senza ridefinire gli oggetti secondari contenuti in quello principale, è possibile impostare il **ObjectExpansion** attributo delle **Alter** comando *ObjectProperties*. Il **ObjectDefinition** proprietà quindi solo deve contenere gli elementi per le proprietà dell'oggetto principale e il **Alter** comando lascia gli oggetti secondari associati all'oggetto principale invariato.  
  
 Per ridefinire gli oggetti secondari per un oggetto principale, è necessario impostare il **ObjectExpansion** dell'attributo *ExpandFull* e la definizione dell'oggetto deve includere tutti gli oggetti secondari contenuti in quello principale. Se il **ObjectDefinition** proprietà delle **Alter** comando non include in modo esplicito un oggetto secondario contenuto in quello principale, viene eliminato l'oggetto secondario non è stato fornito.  
  
### <a name="altering-session-objects"></a>Modifica di oggetti di sessione  
 Per modificare gli oggetti di sessione creati dal **Create** comando, impostare il **ambito** attributo del **Alter** comando *sessione*.  
  
> [!NOTE]  
>  Quando si usa la *sessione* impostazione, il **ObjectDefinition** elemento può contenere solo [dimensione](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl), [cubo](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl), o [ Elemento MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) gli elementi ASSL.  
  
## <a name="creating-or-altering-subordinate-objects"></a>Creazione o modifica di oggetti subordinati  
 Anche se un **Create** oppure **Alter** comando Crea o modifica un solo oggetto principale in primo piano, l'oggetto principale creato o modificato può contenere definizioni all'interno che li racchiude  **ObjectDefinition** proprietà per altri oggetti principali e secondari subordinati. Ad esempio, se si definisce un cubo, si specifica il database padre nella **ParentObject**e nell'ambito della definizione del cubo **ObjectDefinition** è possibile definire gruppi di misure del cubo e all'interno di misure gruppi è possibile definire partizioni per ogni gruppo di misure. Un oggetto secondario può essere definito solo sotto l'oggetto principale che lo contiene. Per altre informazioni sugli oggetti principali e secondarie, vedere [gli oggetti di Database &#40;Analysis Services - dati multidimensionali&#41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md).  
  
## <a name="examples"></a>Esempi  
  
### <a name="description"></a>Descrizione  
 L'esempio seguente crea un'origine dati relazionale che fa riferimento il [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] campione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
### <a name="code"></a>Codice  
  
```  
<Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    </ParentObject>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ImpersonationInfo>  
                <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
            </ImpersonationInfo>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT0S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Create>  
```  
  
### <a name="description"></a>Descrizione  
 Nell'esempio seguente viene modificata l'origine dati relazionale creata nell'esempio precedente per impostare il timeout per la query per l'origine dati su 30 secondi.  
  
### <a name="code"></a>Codice  
  
```  
<Alter ObjectExpansion="ObjectProperties" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DataSourceID>AdventureWorksDW2012</DataSourceID>  
    </Object>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=fr-dwk-02;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT30S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Alter>  
```  
  
### <a name="comments"></a>Commenti  
 Il **ObjectExpansion** attributo il **Alter** comando è stato impostato su *ObjectProperties*. Questa impostazione consente il [ImpersonationInfo](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl) elemento, un oggetto secondario, da escludere dall'origine dati definita **ObjectDefinition**. Le impostazioni di rappresentazione per tale origine dati rimangono pertanto configurate sull'account del servizio, come specificato nel primo esempio.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire il metodo &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)   
 [Sviluppo con Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Sviluppo con XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
