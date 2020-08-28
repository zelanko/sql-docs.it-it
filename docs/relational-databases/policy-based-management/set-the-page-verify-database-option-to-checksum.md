---
title: Impostare l'opzione di database PAGE_VERIFY su CHECKSUM | Microsoft Docs
description: Verificare se l'opzione PAGE_VERIFY è CHECKSUM, che controlla se il motore di database di SQL Server calcola un checksum per assicurare l'integrità dei file di dati.
ms.custom: ''
ms.date: 08/19/2020
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
ms.openlocfilehash: 4dda2b9138882490b1556b9dbb39f71e35767f5f
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646511"
---
# <a name="set-the-page_verify-database-option-to-checksum"></a>Impostazione dell'opzione di database PAGE_VERIFY su CHECKSUM
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Questa regola consente di controllare se l'opzione di database PAGE_VERIFY è impostata su CHECKSUM. Se per l'opzione di database PAGE_VERIFY si specifica CHECKSUM, il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] calcola un checksum sul contenuto dell'intera pagina e archivia il valore nell'intestazione di pagina quando viene scritta una pagina nel disco. Quando si esegue la lettura della pagina dal disco, il checksum viene ricalcolato e confrontato con il valore di checksum archiviato nell'intestazione della pagina. In questo modo viene garantito un livello elevato di integrità dei file di dati.  Se si usa l'opzione PAGE VERIFY CHECKSUM per un database, quando SQL Server rileva una pagina che è stata modificata dopo essere stata scritta su disco, SQL Server segnala il [messaggio 824](../errors-events/mssqlserver-824-database-engine-error.md) dopo averla letta dal disco. 
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 Impostare l'opzione di database PAGE_VERIFY su CHECKSUM. L'uso dell'opzione di database PAGE_VERIFY CHECKSUM può consentire di rilevare in modo più affidabile i problemi di coerenza del database causati dal percorso di I/O del sistema.
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
