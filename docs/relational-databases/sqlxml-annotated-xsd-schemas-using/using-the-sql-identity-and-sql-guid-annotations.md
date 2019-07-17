---
title: 'Usando la: Identity delle annotazioni e | Microsoft Docs'
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
ms.openlocfilehash: 1a6c19e23fc886e15b8e116ca293c4560fded74e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066878"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>Utilizzo delle annotazioni sql:identity e sql:guid
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  È possibile specificare il **: Identity** e **sql:guid** annotazioni in uno schema XSD su qualsiasi nodo che esegue il mapping a una colonna di database di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Mentre il formato dell'updategram supporta il **updg: a-identity** e **updg: GUID** attributi, non presenta il formato DiffGram. Il **updg: a-identity** attributo definisce il comportamento di aggiornamento di una colonna di tipo IDENTITY. Il **updg: GUID** attributo consente di ottenere un valore GUID da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e utilizzarlo nell'updategram. Per altre informazioni ed esempi, vedere [inserimento di dati mediante Updategram XML &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
 Il **: Identity** e **sql:guid** annotazioni estendono questa funzionalità ai DiffGram.  
  
 Per eseguire un DiffGram, è necessario prima convertirlo in updategram. Specificando il **: Identity** e **sql:guid** annotazioni nello schema XSD, vengono di fatto si definisce il comportamento di un updategram. Tutte le annotazioni vengono pertanto descritte nel contesto di un updategram. Le annotazioni possono essere utilizzate sia per i DiffGram che per gli updategram. Per gli updategram è tuttavia già disponibile una modalità di gestione dell'identità e dei valori GUID più potente.  
  
 Il **: Identity** e **sql:guid** le annotazioni possono essere definite in un elemento di contenuto complesso.  
  
## <a name="sqlidentity-annotation"></a>Annotazione sql:identity  
 È possibile specificare il **: Identity** annotazione nello schema XSD su qualsiasi nodo che esegue il mapping a una colonna di database di tipo IDENTITY. Il valore specificato per questa annotazione definisce come viene aggiornata la colonna di tipo IDENTITY (utilizzando il valore fornito nell'updategram per modificare la colonna o ignorando il valore, nel qual caso una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-valore generato viene utilizzato per la colonna).  
  
 Il **: Identity** annotazione può essere assegnata a due valori:  
  
 ignore  
 Indica all'updategram di ignorare qualsiasi valore fornito nell'updategram per la colonna in oggetto e di generare il valore Identity in base a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 useValue  
 Indica all'updategram di utilizzare il valore fornito nell'updategram per aggiornare la colonna di tipo IDENTITY. Un updategram non controlla se la colonna è un valore Identity.  
  
 Se l'updategram specifica un valore per la colonna di tipo IDENTITY, il **: Identity = "useValue"** deve essere specificato nello schema.  
  
## <a name="sqlguid-annotation"></a>Annotazione sql:guid  
 Un valore GUID può essere generato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quindi utilizzato nell'updategram. Nel contesto dei DiffGram, è possibile usare la **sql:guid** annotazione per specificare se utilizzare un valore GUID generato da SQL Server o usare il valore fornito nell'updategram per la colonna.  
  
 Il **sql:guid** annotazione può essere assegnata a due valori:  
  
 generate  
 Specifica che il valore GUID generato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere utilizzato per la colonna specifica nell'operazione di aggiornamento.  
  
 useValue  
 Specifica che per la colonna deve essere utilizzato il valore specificato nell'updategram. Rappresenta il valore predefinito.  
  
  
