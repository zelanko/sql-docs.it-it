---
title: 'Usando la: Identity delle annotazioni e | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
manager: craigg
ms.openlocfilehash: c6135f1b46e9b2312f01b9ff7a7ebdd08d2d34a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013642"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>Utilizzo delle annotazioni sql:identity e sql:guid
  È possibile specificare il `sql:identity` e `sql:guid` annotazioni in uno schema XSD su qualsiasi nodo che esegue il mapping a una colonna di database in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il formato dell'updategram supporta gli attributi `updg:at-identity` e `updg:guid` che invece non vengono supportati dal formato DiffGram. L'attributo `updg:at-identity` definisce il comportamento relativo all'aggiornamento di una colonna di tipo IDENTITY. L'attributo `updg:guid` consente di ottenere un valore GUID da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e di utilizzarlo nell'updategram. Per altre informazioni ed esempi, vedere [inserimento di dati mediante Updategram XML &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
 Le annotazioni `sql:identity` e `sql:guid` estendono questa funzionalità ai DiffGram.  
  
 Per eseguire un DiffGram, è necessario prima convertirlo in updategram. Specificando le annotazioni `sql:identity` e `sql:guid` nello schema XSD, di fatto si definisce il comportamento di un updategram. Tutte le annotazioni vengono pertanto descritte nel contesto di un updategram. Le annotazioni possono essere utilizzate sia per i DiffGram che per gli updategram. Per gli updategram è tuttavia già disponibile una modalità di gestione dell'identità e dei valori GUID più potente.  
  
 Le annotazioni `sql:identity` e `sql:guid` possono essere definite su un elemento di contenuto complesso.  
  
## <a name="sqlidentity-annotation"></a>Annotazione sql:identity  
 È possibile specificare l'annotazione `sql:identity` nello schema XSD su qualsiasi nodo che esegue il mapping a una colonna di database di tipo IDENTITY. Il valore specificato per questa annotazione definisce come viene aggiornata la colonna di tipo IDENTITY (utilizzando il valore fornito nell'updategram per modificare la colonna o ignorando il valore, nel qual caso una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-valore generato viene utilizzato per la colonna).  
  
 All'annotazione `sql:identity` è possibile assegnare due valori:  
  
 ignore  
 Indica all'updategram di ignorare qualsiasi valore fornito nell'updategram per la colonna in oggetto e di generare il valore Identity in base a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 useValue  
 Indica all'updategram di utilizzare il valore fornito nell'updategram per aggiornare la colonna di tipo IDENTITY. Un updategram non controlla se la colonna è un valore Identity.  
  
 Se l'updategram specifica un valore per la colonna di tipo IDENTITY, è necessario specificare `sql:identity="useValue"` nello schema.  
  
## <a name="sqlguid-annotation"></a>Annotazione sql:guid  
 Un valore GUID può essere generato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quindi utilizzato nell'updategram. Nel contesto dei DiffGram è possibile utilizzare l'annotazione `sql:guid` per specificare se utilizzare un valore GUID generato da SQL Server oppure il valore fornito nell'updategram per la colonna specifica.  
  
 All'annotazione `sql:guid` è possibile assegnare due valori:  
  
 generate  
 Specifica che il valore GUID generato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere utilizzato per la colonna specifica nell'operazione di aggiornamento.  
  
 useValue  
 Specifica che per la colonna deve essere utilizzato il valore specificato nell'updategram. Rappresenta il valore predefinito.  
  
  
