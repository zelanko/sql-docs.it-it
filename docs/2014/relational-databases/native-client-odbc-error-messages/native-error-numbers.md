---
title: Numeri di errore nativi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b9612fbd7dd50ffeec812532e25a63eecca26571
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705358"
---
# <a name="native-error-numbers"></a>Numeri di errori nativi
  Per gli errori che si verificano nell'origine dati (restituiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ), il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client restituisce il numero di errore nativo restituito da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per gli errori rilevati dal driver, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client restituisce un numero di errore nativo pari a 0. Per ulteriori informazioni su un elenco di numeri di errore nativi, vedere la colonna Error della tabella di sistema **sysmessages** nel database **Master** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per informazioni sui codici di errore di stato, vedere [SQLSTATE &#40;codici di errore ODBC&#41;](sqlstate-odbc-error-codes.md). Per gli errori restituiti dalla libreria di rete, il numero di errori nativi viene derivato dal software di rete sottostante.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di errori e messaggi](handling-errors-and-messages.md)  
  
  
