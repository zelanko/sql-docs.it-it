---
title: Serializzazione XML da oggetti di Database CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- serialization
- XML serialization [CLR integration]
- common language runtime [SQL Server], XML serialization
- XmlSerializer class
ms.assetid: ac84339b-9384-4710-bebc-01607864a344
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 646d15dc3091323e6e7db2af757640122fb2f0fd
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158477"
---
# <a name="xml-serialization-from-clr-database-objects"></a>Serializzazione XML da oggetti di database CLR
  La serializzazione XML è necessaria in due scenari:  
  
-   Richiamo di servizi Web da oggetti CLR (Common Language Runtime).  
  
-   Conversione in XML di un tipo definito dall'utente.  
  
 Se la serializzazione XML viene eseguita richiamando la classe `XmlSerializer` di solito viene generato un assembly di serializzazione aggiuntivo che viene sottoposto a overload nel progetto con l'assembly di origine. Tuttavia, per motivi di sicurezza, questo overload è disabilitato in CLR. Pertanto, per chiamare un servizio web o eseguire la conversione dal tipo definito dall'utente in XML all'interno [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'assembly deve essere creata manualmente usando uno strumento denominato **Sgen.exe** fornito con .NET Framework che genera le necessarie assembly di serializzazione. Quando si richiama `XmlSerializer`, l'assembly di serializzazione deve essere creato manualmente tramite la seguente procedura:  
  
1.  Eseguire la **Sgen.exe** strumento fornito con .NET Framework SDK per creare l'assembly contenente i serializzatori XML per l'assembly di origine.  
  
2.  Utilizzando l'istruzione `CREATE ASSEMBLY`, registrare in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'assembly generato.  
  
 Per informazioni sugli errori che potrebbero essere visualizzati quando si esegue la serializzazione XML, vedere l'articolo di supporto tecnico Microsoft seguente: ["Cannot load dynamically generated serialization assembly"](https://support.microsoft.com/kb/913668).  
  
 Per informazioni su tipi di dati che non sono supportati da XMLSerializer, vedere Supporto dell'associazione a XML Schema nella documentazione di .NET Framework.  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso ai dati da oggetti di Database CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)   
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
  
