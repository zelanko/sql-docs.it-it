---
title: MSSQLSERVER_1803 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1803 (Database Engine error)
ms.assetid: d4315390-82f1-4c4c-8d1b-1a4989537cca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c1fd65bf2c79c7360f2502975e911aea7ab225d7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62915264"
---
# <a name="mssqlserver_1803"></a>MSSQLSERVER_1803
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|1803|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|NO_SPACE|  
|Testo del messaggio|Istruzione CREATE DATABASE non riuscita. Per contenere una copia del database modello, il file primario deve essere di almeno %d MB.|  
  
## <a name="explanation"></a>Spiegazione  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un database eseguendo una copia del database modello. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rinomina quindi la copia e aumenta le dimensioni del nuovo database fino a quelle richieste. In questo caso l'utente ha tentato di creare un database di dimensioni inferiori rispetto al database modello. L'operazione non è riuscita perché le dimensioni del file di dati primario sono minori rispetto a quelle del database modello.  
  
## <a name="user-action"></a>Azione dell'utente  
 Creare il database aumentando le dimensioni dei file di database. Ridurre quindi il database se si desidera utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o l'istruzione DBCC SHRINKDATABASE.  
  
  
