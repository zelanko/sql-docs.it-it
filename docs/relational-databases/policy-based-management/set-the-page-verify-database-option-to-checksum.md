---
title: Impostare l'opzione di database PAGE_VERIFY su CHECKSUM | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6d0491eb44eb2880927aef006ccc705230ab1940
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021655"
---
# <a name="set-the-pageverify-database-option-to-checksum"></a>Impostazione dell'opzione di database PAGE_VERIFY su CHECKSUM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questa regola consente di controllare se l'opzione di database PAGE_VERIFY è impostata su CHECKSUM. Se per l'opzione di database PAGE_VERIFY si specifica CHECKSUM, il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] calcola un checksum sul contenuto dell'intera pagina e archivia il valore nell'intestazione di pagina quando viene scritta una pagina nel disco. Quando si esegue la lettura della pagina dal disco, il checksum viene ricalcolato e confrontato con il valore di checksum archiviato nell'intestazione della pagina. In questo modo viene garantito un livello elevato di integrità dei file di dati.  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 Impostare l'opzione di database PAGE_VERIFY su CHECKSUM.  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [Opzioni di ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
