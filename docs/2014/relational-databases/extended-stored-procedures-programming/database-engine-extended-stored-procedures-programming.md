---
title: Programmazione di Stored procedure estese | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- gateway applications [SQL Server]
- extended stored procedures [SQL Server], about extended stored procedures
- Open Data Services [SQL Server]
- ODS [SQL Server]
ms.assetid: 561305cd-c803-48af-9eec-2c19f4d311ce
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bc740b25f875b451168a8c051e6f32bd984fbfe6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62514456"
---
# <a name="programming-extended-stored-procedures"></a>Programmazione di stored procedure estese
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 In passato i servizi ODS (Open Data Services) venivano utilizzati per scrivere applicazioni server, come gateway per ambienti di database non SQL Server. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta le parti obsolete dell'API di Open Data Services. Poiché l'unica parte dell'API di Open Data Services originale ancora supportata in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è rappresentata dalle stored procedure estese, l'API è stata rinominata in API Stored procedure estesa.  
  
 Con la comparsa delle più recenti e avanzate tecnologie, ad esempio le query distribuite e l'integrazione con CLR, la necessità di ricorrere alle applicazioni per l'API Stored procedure estesa è stata ampiamente soppiantata.  
  
> [!NOTE]  
>  Se si dispone di applicazioni gateway esistenti, non è possibile utilizzare il file opends60.dll fornito con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per eseguire le applicazioni. Le applicazioni gateway non sono più supportate.  
  
## <a name="extended-stored-procedures-vs-clr-integration"></a>Stored procedure estese rispetto. integrazione CLR  
 Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le stored procedure estese forniscono l'unico meccanismo a disposizione degli sviluppatori delle applicazioni di database per scrivere una logica sul lato server difficile da definire o impossibile da scrivere in [!INCLUDE[tsql](../../includes/tsql-md.md)]. La funzionalità di integrazione con CLR offre un'alternativa più affidabile per la scrittura di tali stored procedure. Grazie all'integrazione con CLR, inoltre, la logica che veniva in genere scritta sotto forma di stored procedure viene spesso definita in modo anche più appropriato sotto forma di funzioni con valori di tabella. Tali funzioni consentono di eseguire query sui risultati restituiti nelle istruzioni SELECT incorporandoli nella clausola FROM.  
  
## <a name="see-also"></a>Vedere anche  
 [Common Language Runtime &#40;CLR&#41; panoramica dell'integrazione](../clr-integration/common-language-runtime-integration-overview.md)   
 [Funzioni CLR con valori di tabella](../clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)  
  
  
