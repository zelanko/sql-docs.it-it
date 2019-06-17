---
title: La gestione degli assembly dell'integrazione CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- database objects [CLR integration], assemblies
- common language runtime [SQL Server], assemblies
- assemblies [CLR integration], managing
ms.assetid: bdbbf325-14f6-460e-a35a-d3861d3c961e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1e65bb5c651862a82d78faede158234d20392c1c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919690"
---
# <a name="managing-clr-integration-assemblies"></a>Gestione degli assembly dell'integrazione con CLR
  Il codice gestito viene compilato e quindi distribuito in unità denominate assembly. Un assembly viene compresso come DLL o file eseguibile (con estensione exe). Mentre un file eseguibile può essere eseguito in modo autonomo, una DLL deve essere ospitata in un'applicazione esistente. Gli assembly DLL gestiti possono essere caricati e ospitati da [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] database utilizzando l'istruzione CREATE ASSEMBLY, prima che possa essere caricato nel processo e utilizzato. Gli assembly possono inoltre essere aggiornati a una versione più recente tramite l'istruzione ALTER ASSEMBLY o rimossi da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite l'istruzione DROP ASSEMBLY.  
  
 Le informazioni sugli assembly vengono archiviate nella tabella `sys.assembly_files` del database in cui è stato installato l'assembly. La tabella `sys.assembly_files` contiene le colonne seguenti.  
  
|colonna|Descrizione|  
|------------|-----------------|  
|assembly_id|Identificatore definito per l'assembly. Questo numero viene assegnato a tutti gli oggetti relativi allo stesso assembly.|  
|NAME|Nome dell'oggetto .|  
|file_id|Numero che identifica ogni oggetto. Al primo oggetto associato a un valore `assembly_id` specifico viene assegnato il valore 1. Se più oggetti sono associati allo stesso valore `assembly_id`, ogni valore `file_id` successivo verrà incrementato di 1.|  
|content|Rappresentazione esadecimale dell'assembly o del file.|  
  
## <a name="in-this-section"></a>In questa sezione  
 [Creazione di un assembly](creating-an-assembly.md)  
 Viene descritta la creazione di assembly CLR SAFE, EXTERNAL_ACCESS e UNSAFE in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Modifica di un assembly](altering-an-assembly.md)  
 Viene descritto l'aggiornamento di assembly CLR in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Eliminazione di un assembly](dropping-an-assembly.md)  
 Viene descritta l'eliminazione di assembly CLR da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza dell'integrazione CLR](../security/clr-integration-security.md)   
 [Sicurezza dall'accesso di codice dell'integrazione con CLR](../security/clr-integration-code-access-security.md)  
  
  
