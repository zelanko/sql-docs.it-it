---
title: Creazione e modifica di oggetti (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [XML for Analysis]
- subordinate objects [XML for Analysis]
- XML for Analysis, objects
- modifying objects
- removing objects
- deleting objects
- XMLA, objects
ms.assetid: a2080867-e130-440c-92eb-f768869f34a8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3dcc6eedc97b3d476d79420b4e067883e17f03d2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62702294"
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
 Quando si creano oggetti tramite il metodo `Create`, è necessario innanzitutto identificare l'oggetto padre che contiene l'oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da creare. Identificare l'oggetto padre, che fornisce un riferimento all'oggetto nel [ParentObject](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) proprietà del `Create` comando. Ogni riferimento all'oggetto contiene gli identificatori dell'oggetto necessari per identificare in modo univoco l'oggetto padre per il comando `Create`. Per altre informazioni sui riferimenti a oggetti, vedere [definizione e identificazione di oggetti &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects).  
  
 Si supponga ad esempio che sia necessario fornire un riferimento a un oggetto per un cubo per creare un nuovo gruppo di misure per il cubo stesso. Il riferimento all'oggetto per il cubo nella proprietà `ParentObject` contiene sia un identificatore di database che un identificatore del cubo poiché lo stesso identificatore del cubo potrebbe essere utilizzato in un database diverso.  
  
 Il [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) elemento contiene elementi di Analysis Services Scripting Language (ASSL) che definiscono l'oggetto principale da creare. Per altre informazioni su ASSL, vedere [lo sviluppo con Analysis Services Scripting Language &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Se si imposta l'attributo `AllowOverwrite` del comando `Create` su true, è possibile sovrascrivere un oggetto principale esistente con l'identificatore specificato. In caso contrario, se un oggetto principale con l'identificatore specificato esiste già nell'oggetto padre si verifica un errore.  
  
 Per altre informazioni sul `Create` comando, vedere [Crea elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla).  
  
### <a name="creating-session-objects"></a>Creazione di oggetti di sessione  
 Gli oggetti di sessione sono oggetti temporanei disponibili solo nella sessione esplicita o implicita utilizzata da un'applicazione client che vengono eliminati quando la sessione è terminata. È possibile creare oggetti di sessione impostando il `Scope` attributo del `Create` comando *sessione*.  
  
> [!NOTE]  
>  Quando si usa la *sessione* impostazione, il `ObjectDefinition` elemento può contenere solo [dimensione](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl), [cubo](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl), o [MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL elementi.  
  
## <a name="altering-objects"></a>Modifica di oggetti  
 Quando si modificano oggetti tramite il `Alter` metodo, è necessario innanzitutto identificare l'oggetto da modificare, fornendo un riferimento all'oggetto nel [oggetto](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) proprietà del `Alter` comando. Ogni riferimento all'oggetto contiene gli identificatori dell'oggetto necessari per identificare in modo univoco l'oggetto per il comando `Alter`. Per altre informazioni sui riferimenti a oggetti, vedere [definizione e identificazione di oggetti &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects).  
  
 Si supponga ad esempio che sia necessario fornire un riferimento a un oggetto per un cubo per modificarne la struttura. Il riferimento all'oggetto per il cubo nella proprietà `Object` contiene sia un identificatore di database che un identificatore del cubo poiché lo stesso identificatore del cubo potrebbe essere utilizzato in un database diverso.  
  
 L'elemento `ObjectDefinition` contiene elementi ASSL che definiscono l'oggetto principale da modificare. Per altre informazioni su ASSL, vedere [lo sviluppo con Analysis Services Scripting Language &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Se si imposta l'attributo `AllowCreate` del comando `Alter` su true, è possibile creare l'oggetto principale specificato qualora non esista. In caso contrario, se un oggetto principale specificato non esiste si verifica un errore.  
  
### <a name="using-the-objectexpansion-attribute"></a>Utilizzo dell'attributo ObjectExpansion  
 Se si siano modificando solo le proprietà dell'oggetto principale senza ridefinire gli oggetti secondari contenuti in quello principale, è possibile impostare il `ObjectExpansion` attributo del `Alter` comando *ObjectProperties*. La proprietà `ObjectDefinition` deve contenere pertanto solo gli elementi per le proprietà dell'oggetto principale e il comando `Alter` non modifica gli oggetti secondari associati all'oggetto principale.  
  
 Per ridefinire gli oggetti secondari per un oggetto principale, è necessario impostare il `ObjectExpansion` dell'attributo *ExpandFull* e la definizione dell'oggetto deve includere tutti gli oggetti secondari contenuti in quello principale. Se la proprietà `ObjectDefinition` del comando `Alter` non include in modo esplicito un oggetto secondario contenuto in quello principale, l'oggetto secondario non incluso viene eliminato.  
  
### <a name="altering-session-objects"></a>Modifica di oggetti di sessione  
 Per modificare gli oggetti di sessione creati dal `Create` comando, impostare il `Scope` attributo delle `Alter` comando *sessione*.  
  
> [!NOTE]  
>  Quando si usa la *sessione* impostazione, il `ObjectDefinition` elemento può contenere solo [dimensione](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl), [cubo](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl), o [MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL elementi.  
  
## <a name="creating-or-altering-subordinate-objects"></a>Creazione o modifica di oggetti subordinati  
 Sebbene un comando `Create` o `Alter` crei o modifichi solo un oggetto principale di livello superiore, l'oggetto principale creato o modificato può includere nella proprietà `ObjectDefinition` che lo contiene definizioni per altri oggetti principali e secondari subordinati. Se si definisce un cubo, ad esempio, si specifica innanzitutto il database padre in `ParentObject`, quindi nella definizione del cubo in `ObjectDefinition` è possibile definire gruppi di misure per il cubo e nei gruppi di misure è possibile definire partizioni per ogni gruppo. Un oggetto secondario può essere definito solo sotto l'oggetto principale che lo contiene. Per altre informazioni sugli oggetti principali e secondarie, vedere [gli oggetti di Database &#40;Analysis Services - dati multidimensionali&#41;](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md).  
  
## <a name="examples"></a>Esempi  
  
### <a name="description"></a>Descrizione  
 L'esempio seguente crea un'origine dati relazionale che fa riferimento il [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] campione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
### <a name="code"></a>Codice  
  
```  
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
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
<Alter ObjectExpansion="ObjectProperties" xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
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
 Il `ObjectExpansion` attributo del `Alter` comando è stato impostato su *ObjectProperties*. Questa impostazione consente il [ImpersonationInfo](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl) elemento, un oggetto secondario, da escludere dall'origine dati definita `ObjectDefinition`. Le impostazioni di rappresentazione per tale origine dati rimangono pertanto configurate sull'account del servizio, come specificato nel primo esempio.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire il metodo &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)   
 [Sviluppo con Analysis Services Scripting Language &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Sviluppo con XMLA in Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
