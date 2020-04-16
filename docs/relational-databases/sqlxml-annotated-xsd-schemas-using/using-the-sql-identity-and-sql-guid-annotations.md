---
title: Utilizzo delle annotazioni sql:identity e sql:guid
description: Informazioni su come usare le annotazioni sql:identity e sql:guid in uno schema XSD per definire il comportamento di un updategram XML.
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
ms.openlocfilehash: f581c1a5c0d925d48df5a16d95cdb141e2d48f83
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388101"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>Utilizzo delle annotazioni sql:identity e sql:guid
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  È possibile specificare le annotazioni **sql:identity** e **sql:guid** in uno schema [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XSD in qualsiasi nodo mappato a una colonna di database in . Mentre il formato updategram supporta gli attributi **updg:at-identity** e **updg:guid,** il formato DiffGram non lo supporta. L'attributo **updg:at-identity** definisce il comportamento nell'aggiornamento di una colonna di tipo IDENTITY. L'attributo **updg:guid** consente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ottenere un valore GUID da e utilizzarlo nell'updategram. Per ulteriori informazioni ed esempi di lavoro, vedere [Inserimento di dati tramite updategrammi XML &#40;&#41;SQLXML 4.0. ](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)  
  
 Le annotazioni **sql:identity** e **sql:guid** estendono questa funzionalità a DiffGrams.  
  
 Per eseguire un DiffGram, è necessario prima convertirlo in updategram. Specificando le annotazioni **sql:identity** e **sql:guid** nello schema XSD, si definisce infatti il comportamento di un updategram. Tutte le annotazioni vengono pertanto descritte nel contesto di un updategram. Le annotazioni possono essere utilizzate sia per i DiffGram che per gli updategram. Per gli updategram è tuttavia già disponibile una modalità di gestione dell'identità e dei valori GUID più potente.  
  
 Le annotazioni **sql:identity** e **sql:guid** possono essere definite in un elemento di contenuto complesso.  
  
## <a name="sqlidentity-annotation"></a>Annotazione sql:identity  
 È possibile specificare l'annotazione **sql:identity** nello schema XSD in qualsiasi nodo mappato a una colonna di database di tipo IDENTITY. Il valore specificato per questa annotazione definisce la modalità di aggiornamento della colonna di tipo IDENTITY (utilizzando il valore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]fornito nell'updategram per modificare la colonna o ignorando il valore, nel qual caso viene utilizzato un valore generato per questa colonna).  
  
 All'annotazione sql:identity possono essere assegnati due valori:The **sql:identity** annotation can be assigned two values:  
  
 ignore  
 Indica all'updategram di ignorare qualsiasi valore fornito nell'updategram per la colonna in oggetto e di generare il valore Identity in base a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 useValue  
 Indica all'updategram di utilizzare il valore fornito nell'updategram per aggiornare la colonna di tipo IDENTITY. Un updategram non controlla se la colonna è un valore Identity.  
  
 Se l'updategram specifica un valore per la colonna di tipo IDENTITY, è necessario specificare **sql:identity:"useValue"** nello schema.  
  
## <a name="sqlguid-annotation"></a>Annotazione sql:guid  
 Un valore GUID può essere generato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quindi utilizzato nell'updategram. Nel contesto di DiffGrams, è possibile utilizzare l'annotazione **sql:guid** per specificare se utilizzare un valore GUID generato da SQL ServerSQL Server o utilizzare il valore fornito nell'updategram per tale colonna.  
  
 All'annotazione sql:guid possono essere assegnati due valori:The **sql:guid** annotation can be assigned two values:  
  
 generate  
 Specifica che il valore GUID generato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere utilizzato per la colonna specifica nell'operazione di aggiornamento.  
  
 useValue  
 Specifica che per la colonna deve essere utilizzato il valore specificato nell'updategram. Si tratta del valore predefinito.  
  
  
