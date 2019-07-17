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
ms.openlocfilehash: bde493edbc6d677b27ef72a24736b504959a7b59
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114133"
---
# <a name="step-5-commit-the-transaction"></a>Passaggio 5: Eseguire il commit della transazione
Il passaggio successivo è eseguire il commit della transazione, come illustrato nella figura seguente.  
  
 ![Viene illustrato come eseguire il commit di una transazione](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 Il quinto passaggio consiste nel chiamare **SQLEndTran** per eseguire il commit o rollback della transazione. L'applicazione esegue questo passaggio solo se la modalità di commit delle transazioni impostata su commit manuale; Se la modalità di commit delle transazioni è commit automatico, ovvero l'impostazione predefinita, viene automaticamente eseguito il commit della transazione quando viene eseguita l'istruzione. Per altre informazioni, vedere [transazioni](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Per eseguire un'istruzione in una nuova transazione, l'applicazione torna al passaggio 3. Per disconnettersi dall'origine dati, l'applicazione procede al passaggio 6.
