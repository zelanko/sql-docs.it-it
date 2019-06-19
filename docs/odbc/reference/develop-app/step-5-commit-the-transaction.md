---
title: 'Passaggio 5: Eseguire il commit della transazione | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 341f34afa1dbe65f4b83a46f461bb93f4fb4f4c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63148953"
---
# <a name="step-5-commit-the-transaction"></a>Passaggio 5: Eseguire il commit della transazione
Il passaggio successivo è eseguire il commit della transazione, come illustrato nella figura seguente.  
  
 ![Viene illustrato come eseguire il commit di una transazione](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 Il quinto passaggio consiste nel chiamare **SQLEndTran** per eseguire il commit o rollback della transazione. L'applicazione esegue questo passaggio solo se la modalità di commit delle transazioni impostata su commit manuale; Se la modalità di commit delle transazioni è commit automatico, ovvero l'impostazione predefinita, viene automaticamente eseguito il commit della transazione quando viene eseguita l'istruzione. Per altre informazioni, vedere [transazioni](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Per eseguire un'istruzione in una nuova transazione, l'applicazione torna al passaggio 3. Per disconnettersi dall'origine dati, l'applicazione procede al passaggio 6.
