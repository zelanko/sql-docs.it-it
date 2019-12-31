---
title: Utilizzo delle annotazioni sql:identity e sql:guid
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:guid
- annotated XSD schemas, IDENTITY-type columns
- annotated XSD schemas, GUID values
- DiffGrams [SQLXML], annotations
- identity annotation
- XSD schemas [SQLXML], GUID values
- GUIDs [SQLXML]
- guid annotation
- sql:identity
- IDENTITY-type column
- XSD schemas [SQLXML], IDENTITY-type columns
- updategrams [SQLXML], GUID values
ms.assetid: 7661dfd0-6573-4692-a8f1-3597adcd33c4
author: MightyPen
ms.author: genemi
ms.reviewer: ''
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 50483d7f6f84371b42bf0c79fbc74a1f85a65eab
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246817"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>Utilizzo delle annotazioni sql:identity e sql:guid
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  È possibile specificare le annotazioni **SQL: Identity** e **SQL: GUID** in uno schema XSD su qualsiasi nodo che esegue il mapping a una [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]colonna del database in. Mentre il formato dell'updategram supporta gli attributi **attributo updg: at-identity** e **attributo updg: GUID** , il formato DiffGram non è supportato. L'attributo **attributo updg: at-identity** definisce il comportamento nell'aggiornamento di una colonna di tipo Identity. L'attributo **attributo updg: GUID** consente di ottenere un valore GUID da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e di utilizzarlo nell'updategram. Per ulteriori informazioni ed esempi reali, vedere [inserimento di dati mediante UPDATEGRAM XML &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
 Le annotazioni **SQL: Identity** e **SQL: GUID** estendono questa funzionalità a DiffGram.  
  
 Per eseguire un DiffGram, è necessario prima convertirlo in updategram. Specificando le annotazioni **SQL: Identity** e **SQL: GUID** nello schema XSD, è in effetti necessario definire il comportamento di un updategram. Tutte le annotazioni vengono pertanto descritte nel contesto di un updategram. Le annotazioni possono essere utilizzate sia per i DiffGram che per gli updategram. Per gli updategram è tuttavia già disponibile una modalità di gestione dell'identità e dei valori GUID più potente.  
  
 Le annotazioni **SQL: Identity** e **SQL: GUID** possono essere definite su un elemento di contenuto complesso.  
  
## <a name="sqlidentity-annotation"></a>Annotazione sql:identity  
 È possibile specificare l'annotazione **SQL: Identity** nello schema XSD su qualsiasi nodo che esegue il mapping a una colonna di database di tipo Identity. Il valore specificato per questa annotazione definisce il modo in cui viene aggiornata la colonna di tipo IDENTITY, usando il valore fornito nell'updategram per modificare la colonna o ignorando il valore, nel qual caso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]viene usato un valore generato da per questa colonna.  
  
 All'annotazione **SQL: Identity** possono essere assegnati due valori:  
  
 ignore  
 Indica all'updategram di ignorare qualsiasi valore fornito nell'updategram per la colonna in oggetto e di generare il valore Identity in base a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 useValue  
 Indica all'updategram di utilizzare il valore fornito nell'updategram per aggiornare la colonna di tipo IDENTITY. Un updategram non controlla se la colonna è un valore Identity.  
  
 Se l'updategram specifica un valore per la colonna di tipo IDENTITY, è necessario specificare **SQL: Identity = "useValue"** nello schema.  
  
## <a name="sqlguid-annotation"></a>Annotazione sql:guid  
 Un valore GUID può essere generato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quindi utilizzato nell'updategram. Nel contesto di DiffGram, è possibile utilizzare l'annotazione **SQL: GUID** per specificare se utilizzare un valore GUID generato da SQL Server o utilizzare il valore fornito nell'updategram per la colonna.  
  
 All'annotazione **SQL: GUID** è possibile assegnare due valori:  
  
 generate  
 Specifica che il valore GUID generato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere utilizzato per la colonna specifica nell'operazione di aggiornamento.  
  
 useValue  
 Specifica che per la colonna deve essere utilizzato il valore specificato nell'updategram. Questo è il valore predefinito.  
  
  
