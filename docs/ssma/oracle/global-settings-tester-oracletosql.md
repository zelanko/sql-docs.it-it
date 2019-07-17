---
title: Impostazioni globali (Tester) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4acc0f2a-85ba-4c99-856a-89030f5c418e
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: f7e421774d3a09622835b181d5c053c994e905ee
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264407"
---
# <a name="global-settings-tester-oracletosql"></a>Impostazioni globali (tester) (OracleToSQL)
Utilizzare la pagina di Tester della **Global Settings** finestra di dialogo per specificare le impostazioni per Tester SSMA.  
  
Per accedere a impostazioni di Tester, scegliere il **strumenti** dal menu **impostazioni globali**e fare clic su **Tester** nella parte inferiore del riquadro di sinistra.  
  
## <a name="options"></a>Opzioni  
**Analisi oggetto testabili**  
Questa impostazione specifica se eseguire l'analisi degli oggetti da testare. Selezionare **Sì** se si desidera che il Tester di SSMA per analizzare e controllare automaticamente se gli oggetti dipendenti. Set di opzioni predefinito è **Sì**.  
  
Le opzioni seguenti sono disponibili per questa impostazione:  
  
1.  Yes  
  
2.  No  
  
**Tabelle ausiliarie modalità risparmio**  
Questa impostazione specifica come salvare le tabelle ausiliarie interne create durante l'esecuzione del test case. Per questa particolare impostazione possibile è possibile impostare le opzioni seguenti:  
  
1.  Elimina sempre  
  
2.  Salva sempre  
  
3.  Se il confronto di tabella non è stato possibile salvare  
  
4.  Chiedere a utente se il confronto di tabella non è riuscita  
  
Impostata l'opzione predefinita è: **Elimina sempre**.  
  
**Eseguire il rollback di dati**  
Questa impostazione specifica se eseguire un'operazione di rollback dopo l'esecuzione di ogni test case. Set di opzioni predefinito è **No**.  
  
Le opzioni seguenti sono disponibili per questa impostazione:  
  
1.  Yes  
  
2.  No  
  
**Arrestare l'esecuzione di test dopo il primo errore**  
Questa impostazione specifica se interrompere l'esecuzione test case corrente, se si è verificato un errore durante l'esecuzione. Set di opzioni predefinito è **Sì**.  
  
Le opzioni seguenti sono disponibili per questa impostazione:  
  
1.  Yes  
  
2.  No  
  
## <a name="see-also"></a>Vedere anche  
[Completamento della preparazione del Test Case &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
