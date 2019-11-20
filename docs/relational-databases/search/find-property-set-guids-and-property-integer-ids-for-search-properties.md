---
title: Trovare GUID del set di proprietà e ID di tipo integer delle proprietà per le proprietà di ricerca
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], configuring
ms.assetid: 7db79165-8bcc-4be6-8d40-12d44deda79f
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 3b950557c3c5c22968cffa4be0b4565ddedb293c
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056525"
---
# <a name="find-property-set-guids-and-property-integer-ids-for-search-properties"></a>Trovare GUID del set di proprietà e ID di tipo integer delle proprietà per le proprietà di ricerca
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In questo argomento viene illustrato come ottenere i valori richiesti prima di poter aggiungere una proprietà a un elenco delle proprietà di ricerca e abilitarlo per la ricerca full-text. In questi valori sono inclusi il GUID del set di proprietà e l'identificatore di tipo integer di una proprietà del documento.  
  
 Le proprietà del documento estratte usando filtri IFilter dai dati binari, vale a dire i dati archiviati in una colonna di tipi di dati **varbinary**, **varbinary(max)** (incluso **FILESTREAM**) o **image**, possono essere rese disponibili per la ricerca full-text. Per consentire la ricerca in una proprietà estratta, è necessario aggiungere la proprietà manualmente a un elenco delle proprietà di ricerca. È inoltre necessario che l'elenco delle proprietà di ricerca sia associato a uno o più indici full-text. Per altre informazioni, vedere [Eseguire ricerche nelle proprietà dei documenti con elenchi delle proprietà di ricerca](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
 Per poter aggiungere una proprietà disponibile a un elenco di proprietà, è necessario trovare due informazioni sulla proprietà:  
  
-   GUID del set di proprietà della proprietà.  
  
-   ID di tipo integer della proprietà.  
  
 Quando si aggiunge una proprietà a un elenco delle proprietà, è necessario fornire anche un nome e una descrizione. Non è tuttavia necessario utilizzare il nome canonico e la descrizione della proprietà.  
  
 In questo argomento vengono descritti i metodi di uso comune per trovare informazioni sulle proprietà disponibili, in particolare sulle proprietà definite da Microsoft. Per informazioni sulle proprietà definite da terze parti, fare riferimento alla documentazione di terze parti o contattare il fornitore.  
  
##  <a name="wellknown"></a> Ricerca di informazioni sulle proprietà Microsoft note e ampiamente utilizzate  
 Microsoft definisce centinaia di proprietà del documento da utilizzare in molti contesti, ma solo un piccolo subset delle proprietà disponibili viene utilizzato da ogni formato di file. Tra le proprietà di Windows utilizzate di frequente è presente un piccolo set di proprietà generiche. Nella tabella seguente sono illustrati alcuni esempi di proprietà generiche note. Nella tabella sono indicati il nome noto, il nome canonico di Windows (in base alla descrizione della proprietà pubblicata da Microsoft), il GUID del set di proprietà, l'identificatore di tipo integer della proprietà e una breve descrizione.  
  
|Nome noto|Nome canonico di Windows.|GUID set di proprietà|ID di tipo integer|Descrizione|  
|----------------------|----------------------------|-----------------------|----------------|-----------------|  
|Autori|**System.Author**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|4|Autore o autori di un elemento specificato.|  
|Tag|**System.Keywords**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|5|Set di parole chiave (note anche come tag) assegnate all'elemento.|  
|Tipo|**System.PerceivedType**|28636AA6-953D-11D2-B5D6-00C04FD918D0|9|Tipo di file percepito in base al relativo tipo canonico.|  
|Title|**System.Title**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|2|Titolo dell'elemento. Ad esempio, il titolo di un documento, l'oggetto di un messaggio, la didascalia di una foto o il nome di un brano musicale.|  
  
 Per favorire la coerenza fra formati di file, Microsoft ha identificato subset di proprietà del documento ad alta priorità e di utilizzo frequente per diverse categorie di documenti, quali comunicazioni, contatti, documenti, file musicali, immagini e video. Per altre informazioni sulle principali proprietà classificate per ogni categoria, vedere la pagina [System-Defined Properties for Custom File Formats](https://go.microsoft.com/fwlink/?LinkId=144336) (Proprietà definite dal sistema per formati di file personalizzati) nella documentazione di Windows Search.  
  
 Un formato di file specifico potrebbe implementare proprietà di tre tipi:  
  
-   Proprietà generiche definite da [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
-   Proprietà specifiche della categoria definite da [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
-   Proprietà personalizzate specifiche dell'applicazione definite dal fornitore di software.  
  
##  <a name="filtdump"></a> Ricerca di informazioni sulle proprietà disponibili tramite FILTDUMP.EXE  
 Per conoscere le proprietà individuate ed estratte da un filtro IFilter installato, è possibile installare ed eseguire l'utilità **filtdump.exe** , che fa parte di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows SDK.  
  
 Dal prompt dei comandi eseguire **filtdump.exe** e fornire un argomento singolo. Questo argomento corrisponde al nome di un singolo file che dispone di un tipo di file per il quale viene installato un filtro IFilter. Tramite l'utilità viene visualizzato un elenco di tutte le proprietà individuate da IFilter nel documento, con i relativi GUID del set di proprietà, gli ID di tipo integer e informazioni aggiuntive.  
  
 Per informazioni sull'installazione del software, vedere [Microsoft Windows SDK per Windows 7 e .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=8279). Dopo aver scaricato e installato SDK, cercare nelle seguenti cartelle l'utilità filtdump.exe.  
  
-   Per la versione a 64 bit, vedere in `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin\x64`.  
  
-   Per la versione a 32 bit, vedere in `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin`.  
  
##  <a name="propdesc"></a> Individuazione di valori per una proprietà di ricerca dalla descrizione di una proprietà di Windows  
 Per una proprietà di ricerca di Windows nota, è possibile ottenere le informazioni necessarie dagli attributi **formatID** e **propID** della descrizione della proprietà (**propertyDescription**).  
  
 Nell'esempio seguente viene illustrata la parte rilevante della descrizione di una tipica proprietà Microsoft, in questo caso la proprietà `System.Author` . Con l'attributo `formatID` si specifica il GUID del set di proprietà, `F29F85E0-4FF9-1068-AB91-08002B27B3D9`, e con l'attributo `propID` si specifica l'ID di tipo integer della proprietà, `4.` Si noti che con l'attributo `name` si specifica il nome canonico della proprietà di Windows, `System.Author`. In questo esempio vengono omesse le parti della descrizione della proprietà non rilevanti.  
  
```  
.  
propertyDescription  
name = System.Author  
...  
formatID = F29F85E0-4FF9-1068-AB91-08002B27B3D9  
propID = 4  
...  
```  
  
 Per la descrizione completa della proprietà, vedere [System.Author](https://go.microsoft.com/fwlink/?LinkId=144337) nella documentazione di Windows Search.  
  
 Per un elenco completo delle proprietà di Windows, vedere [Proprietà di Windows](https://go.microsoft.com/fwlink/?LinkId=215013)nella documentazione di Windows Search.  
  
##  <a name="examples"></a> Aggiunta di una proprietà a un elenco delle proprietà di ricerca  
 Nell'esempio seguente viene illustrato come aggiungere una proprietà a un elenco delle proprietà di ricerca. L'esempio usa un'istruzione [ALTER SEARCH PROPERTY LIST](../../t-sql/statements/alter-search-property-list-transact-sql.md) per aggiungere la proprietà `System.Author` a un elenco delle proprietà di ricerca denominato `PropertyList1`e fornisce il nome descrittivo per la proprietà `Author`.  
  
```  
ALTER SEARCH PROPERTY LIST PropertyList1   
  ADD 'Author'  
    WITH (  
          PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9',  
          PROPERTY_INT_ID = 4,   
          PROPERTY_DESCRIPTION = 'System.Author - the author or authors of the item'   
         )  
GO  
```  
  
 Per altre informazioni sulla creazione di un elenco delle proprietà di ricerca e la relativa associazione a un indice full-text, vedere [Eseguire ricerche nelle proprietà dei documenti con elenchi delle proprietà di ricerca](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire ricerche nelle proprietà dei documenti con elenchi delle proprietà di ricerca](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [Configurazione e gestione di filtri per la ricerca](../../relational-databases/search/configure-and-manage-filters-for-search.md)  
  
  
