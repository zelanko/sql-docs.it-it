---
description: 'Passaggio 5: Eseguire il commit della transazione'
title: 'Passaggio 5: eseguire il commit della transazione | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], committing transactions
- committing transactions [ODBC]
- transaction commit [ODBC]
ms.assetid: 311685e2-f7b5-4ddc-8020-59380cd2f035
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4cc3a73e5cfc564992795ab6b18759b1066288c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88385897"
---
# <a name="step-5-commit-the-transaction"></a>Passaggio 5: Eseguire il commit della transazione
Il passaggio successivo consiste nell'eseguire il commit della transazione, come illustrato nella figura seguente.  
  
 ![Come eseguire il commit di una transazione](../../../odbc/reference/develop-app/media/pr16.gif "PR16")  
  
 Il quinto passaggio consiste nel chiamare **SQLEndTran** per eseguire il commit o il rollback della transazione. L'applicazione esegue questo passaggio solo se imposta la modalità di commit delle transazioni su Manual-commit; Se la modalità di commit della transazione è commit automatico, ovvero l'impostazione predefinita, viene eseguito automaticamente il commit della transazione quando viene eseguita l'istruzione. Per altre informazioni, vedere [Transazioni](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Per eseguire un'istruzione in una nuova transazione, l'applicazione torna al passaggio 3. Per disconnettersi dall'origine dati, l'applicazione continua con il passaggio 6.
