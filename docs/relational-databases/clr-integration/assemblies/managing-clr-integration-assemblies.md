---
title: Gestione degli assembly di integrazione CLR | Microsoft Docs
description: È possibile ospitare assembly DLL gestiti in SQL Server.  È possibile registrare, modificare ed eliminare assembly e gestire anche file e autorizzazioni associati.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 84f10e104754019e67255b1a031e228a9ff4c48e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899583"
---
# <a name="managing-clr-integration-assemblies"></a>Gestione degli assembly dell'integrazione con CLR
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Il codice gestito viene compilato e quindi distribuito in unità denominate assembly. Un assembly viene compresso come DLL o file eseguibile (con estensione exe). Mentre un file eseguibile può essere eseguito in modo autonomo, una DLL deve essere ospitata in un'applicazione esistente. Gli assembly DLL gestiti possono essere caricati e ospitati da [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] richiede che si registri l'assembly in un database [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzando l'istruzione CREATE ASSEMBLY, prima che possa essere caricato nel processo e usato. Gli assembly possono inoltre essere aggiornati a una versione più recente tramite l'istruzione ALTER ASSEMBLY o rimossi da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite l'istruzione DROP ASSEMBLY.  
  
 Le informazioni sull'assembly vengono archiviate nella tabella **sys. assembly_files** nel database in cui è stato installato l'assembly. La tabella **sys. assembly_files** contiene le colonne seguenti.  
  
|Colonna|Descrizione|  
|------------|-----------------|  
|assembly_id|Identificatore definito per l'assembly. Questo numero viene assegnato a tutti gli oggetti relativi allo stesso assembly.|  
|name|Nome dell'oggetto .|  
|file_id|Numero che identifica ogni oggetto, con il primo oggetto associato a un dato **assembly_id** a cui viene assegnato il valore 1. Se più oggetti sono associati allo stesso **assembly_id**, ogni valore **file_id** successivo viene incrementato di 1.|  
|contenuto|Rappresentazione esadecimale dell'assembly o del file.|  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Creazione di un assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
 Viene descritta la creazione di assembly CLR SAFE, EXTERNAL_ACCESS e UNSAFE in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Modifica di un assembly](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)  
 Viene descritto l'aggiornamento di assembly CLR in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Eliminazione di un assembly](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)  
 Viene descritta l'eliminazione di assembly CLR da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza dell'integrazione con CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Sicurezza da accesso di codice dell'integrazione con CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
  
  
