---
description: Utilizzo della copia di facet della gestione basata su criteri
title: Usare la copia di facet della gestione basata su criteri | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- viewing Policy-Based Management facets
- facets [Policy-Based Management], copying
- facets [Policy-Based Management], viewing
- copying Policy-Based Management facets
ms.assetid: 88d025c4-07c2-4e4d-8634-204249a8c82c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d785b99fd933cc0209df8ecb0674e65e0d340ea9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475596"
---
# <a name="working-with-policy-based-management-facets"></a>Utilizzo della copia di facet della gestione basata su criteri
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Un facet di gestione basata su criteri è un set di proprietà logiche correlate a un'area di interesse di gestione. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha diversi facet predefiniti. Il facet di gestione della superficie di attacco, ad esempio, definisce come proprietà le funzionalità disabilitate per impostazione predefinita.  
  
 Quando si gestiscono molti ambienti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] simili, è possibile configurare un facet in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], copiare lo stato del facet in un file, quindi importare il file come criteri in un'altra istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Una volta convertito lo stato in criteri, è possibile applicare i criteri ad altre istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nonché ad altri oggetti delle istanze, database o oggetti di database.  
  
 In questo argomento viene descritto come copiare lo stato di un facet in un file XML.  
  
##  <a name="permissions"></a><a name="BeforeYouBegin"></a> Autorizzazioni  
 Le procedure descritte in questo argomento richiedono l'appartenenza al ruolo PolicyAdministratorRole nel database msdb.  
  
## <a name="viewing-and-copying-facet-states"></a>Visualizzazione e copia di stati di un facet  
 [Visualizzare i facet della gestione basata su criteri in un oggetto di SQL Server](../../relational-databases/policy-based-management/view-the-policy-based-management-facets-on-a-sql-server-object.md)  
  
 [Copiare lo stato di un facet della gestione basata su criteri in un file XML](../../relational-databases/policy-based-management/copy-a-policy-based-management-facet-state-to-an-xml-file.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione di server tramite la gestione basata su criteri](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
