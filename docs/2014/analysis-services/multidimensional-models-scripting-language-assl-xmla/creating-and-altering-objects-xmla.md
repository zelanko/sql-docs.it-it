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
ms.openlocfilehash: 2390c0b921368e7e06f0e5563a7eb59769d99c17
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545029"
---
# <a name="creating-and-altering-objects-xmla"></a>Creazione e modifica di oggetti (XMLA)
  Gli oggetti principali possono essere creati, modificati ed eliminati in modo indipendente. Di seguito vengono elencati gli oggetti principali:  
  
-   Server  
  
-   Database  
  
-   Dimensioni  
  
-   Cubi  
  
-   Gruppi di misure  
  
-   Partizioni  
  
-   Prospettive  
  
-   Modelli di data mining  
  
-   Ruoli  
  
-   Comandi associati a un server o a un database  
  
-   Origini dati  
  
 Usare il comando [create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) per creare un oggetto principale in un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e il comando [ALTER](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) per modificare un oggetto principale esistente in un'istanza di. Entrambi i comandi vengono eseguiti usando il metodo [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) .  
  
## <a name="creating-objects"></a>Creazione di oggetti  
 Quando si creano oggetti tramite il metodo `Create`, è necessario innanzitutto identificare l'oggetto padre che contiene l'oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da creare. Per identificare l'oggetto padre, fornire un riferimento all'oggetto nella proprietà [ParentObject](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) del `Create` comando. Ogni riferimento all'oggetto contiene gli identificatori dell'oggetto necessari per identificare in modo univoco l'oggetto padre per il comando `Create`. Per ulteriori informazioni sui riferimenti a oggetti, vedere [definizione e identificazione di oggetti &#40;&#41;XMLA ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects).  
  
 Si supponga ad esempio che sia necessario fornire un riferimento a un oggetto per un cubo per creare un nuovo gruppo di misure per il cubo stesso. Il riferimento all'oggetto per il cubo nella proprietà `ParentObject` contiene sia un identificatore di database che un identificatore del cubo poiché lo stesso identificatore del cubo potrebbe essere utilizzato in un database diverso.  
  
 L'elemento [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) contiene Analysis Services elementi ASSL (Scripting Language) che definiscono l'oggetto principale da creare. Per ulteriori informazioni su ASSL, vedere [sviluppo con Analysis Services linguaggio di scripting &#40;assl&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Se si imposta l'attributo `AllowOverwrite` del comando `Create` su true, è possibile sovrascrivere un oggetto principale esistente con l'identificatore specificato. In caso contrario, se un oggetto principale con l'identificatore specificato esiste già nell'oggetto padre si verifica un errore.  
  
 Per ulteriori informazioni sul `Create` comando, vedere [Create element &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla).  
  
### <a name="creating-session-objects"></a>Creazione di oggetti di sessione  
 Gli oggetti di sessione sono oggetti temporanei disponibili solo nella sessione esplicita o implicita utilizzata da un'applicazione client che vengono eliminati quando la sessione è terminata. È possibile creare oggetti sessione impostando l' `Scope` attributo del `Create` comando su *sessione*.  
  
> [!NOTE]  
>  Quando si utilizza l'impostazione della *sessione* , l' `ObjectDefinition` elemento può contenere solo elementi ASSL di [dimensione](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl), [cubo](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)o [MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) .  
  
## <a name="altering-objects"></a>Modifica di oggetti  
 Quando si modificano gli oggetti usando il `Alter` metodo, è necessario innanzitutto identificare l'oggetto da modificare fornendo un riferimento a un oggetto nella proprietà [Object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) del `Alter` comando. Ogni riferimento all'oggetto contiene gli identificatori dell'oggetto necessari per identificare in modo univoco l'oggetto per il comando `Alter`. Per ulteriori informazioni sui riferimenti a oggetti, vedere [definizione e identificazione di oggetti &#40;&#41;XMLA ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects).  
  
 Si supponga ad esempio che sia necessario fornire un riferimento a un oggetto per un cubo per modificarne la struttura. Il riferimento all'oggetto per il cubo nella proprietà `Object` contiene sia un identificatore di database che un identificatore del cubo poiché lo stesso identificatore del cubo potrebbe essere utilizzato in un database diverso.  
  
 L'elemento `ObjectDefinition` contiene elementi ASSL che definiscono l'oggetto principale da modificare. Per ulteriori informazioni su ASSL, vedere [sviluppo con Analysis Services linguaggio di scripting &#40;assl&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Se si imposta l'attributo `AllowCreate` del comando `Alter` su true, è possibile creare l'oggetto principale specificato qualora non esista. In caso contrario, se un oggetto principale specificato non esiste si verifica un errore.  
  
### <a name="using-the-objectexpansion-attribute"></a>Utilizzo dell'attributo ObjectExpansion  
 Se si modificano solo le proprietà dell'oggetto principale e non si ridefiniscono gli oggetti secondari contenuti nell'oggetto principale, è possibile impostare l' `ObjectExpansion` attributo del `Alter` comando su *ObjectProperties*. La proprietà `ObjectDefinition` deve contenere pertanto solo gli elementi per le proprietà dell'oggetto principale e il comando `Alter` non modifica gli oggetti secondari associati all'oggetto principale.  
  
 Per ridefinire gli oggetti secondari per un oggetto principale, è necessario impostare l' `ObjectExpansion` attributo su *ExpandFull* e la definizione dell'oggetto deve includere tutti gli oggetti secondari contenuti nell'oggetto principale. Se la proprietà `ObjectDefinition` del comando `Alter` non include in modo esplicito un oggetto secondario contenuto in quello principale, l'oggetto secondario non incluso viene eliminato.  
  
### <a name="altering-session-objects"></a>Modifica di oggetti di sessione  
 Per modificare gli oggetti sessione creati dal `Create` comando, impostare l' `Scope` attributo del `Alter` comando su *sessione*.  
  
> [!NOTE]  
>  Quando si utilizza l'impostazione della *sessione* , l' `ObjectDefinition` elemento può contenere solo elementi ASSL di [dimensione](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl), [cubo](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)o [MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) .  
  
## <a name="creating-or-altering-subordinate-objects"></a>Creazione o modifica di oggetti subordinati  
 Sebbene un comando `Create` o `Alter` crei o modifichi solo un oggetto principale di livello superiore, l'oggetto principale creato o modificato può includere nella proprietà `ObjectDefinition` che lo contiene definizioni per altri oggetti principali e secondari subordinati. Se si definisce un cubo, ad esempio, si specifica innanzitutto il database padre in `ParentObject`, quindi nella definizione del cubo in `ObjectDefinition` è possibile definire gruppi di misure per il cubo e nei gruppi di misure è possibile definire partizioni per ogni gruppo. Un oggetto secondario può essere definito solo sotto l'oggetto principale che lo contiene. Per ulteriori informazioni sugli oggetti principali e secondari, vedere [oggetti di Database &#40;Analysis Services-&#41;di dati multidimensionali ](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md).  
  
## <a name="examples"></a>Esempi  
  
### <a name="description"></a>Descrizione  
 Nell'esempio seguente viene creata un'origine dati relazionale che fa riferimento al [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] database di esempio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
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
 L' `ObjectExpansion` attributo del `Alter` comando è stato impostato su *ObjectProperties*. Questa impostazione consente di escludere l'elemento [ImpersonationInfo](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl) , un oggetto secondario, dall'origine dati definita in `ObjectDefinition` . Le impostazioni di rappresentazione per tale origine dati rimangono pertanto configurate sull'account del servizio, come specificato nel primo esempio.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Execute &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)   
 [Sviluppo con Analysis Services linguaggio di scripting &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Sviluppo con XMLA in Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
