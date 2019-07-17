---
title: Risoluzione dei problemi (Driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI [ODBC]
- troubleshooting Visual FoxPro ODBC driver [ODBC]
- remote views [ODBC]
- multitiered views [ODBC]
- parameterized views [ODBC], Visual FoxPro ODBC driver
- fetches [ODBC], Visual FoxPro ODBC driver
- positioned updates [ODBC]
- background fetching [ODBC]
ms.assetid: fd478dd8-666a-4f0a-a2d6-b94e81cbbe4b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4eeb6210b9bce124e16a1b4e666dee03c1d992be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912379"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>Risoluzione dei problemi (driver ODBC Visual FoxPro)
Le sezioni seguenti illustrano come migliorare le prestazioni e risolvere i problemi che possono verificarsi quando si usa il Driver ODBC Visual FoxPro.  
  
## <a name="accessing-parameterized-views"></a>L'accesso a viste con parametri  
 Le viste con parametri in un database di Visual FoxPro usando il driver non è possibile accedere. Una vista con parametri crea una clausola WHERE in SQL della vista **seleziona** istruzione che limita i record scaricati a quei record che soddisfano le condizioni della clausola WHERE creata usando il valore specificato per il parametro. Poiché il driver non supporta il passaggio di parametri per la visualizzazione, i tentativi di accesso di una vista con parametri utilizzando il driver avrà esito negativo.  
  
 Il valore del parametro può essere fornito in fase di esecuzione o a livello di codice passato alla visualizzazione.  
  
## <a name="accessing-remote-views"></a>Accesso alle visualizzazioni Remote  
 Non è possibile accedere visualizzazioni remote in un database di Visual FoxPro usando il driver. Visualizzazioni remote sono che accedono a dati non FoxPro o una combinazione di FoxPro e i dati non FoxPro. Per accedere alle viste remote, utilizzare Visual FoxPro.  
  
## <a name="deleting-records"></a>L'eliminazione di record  
 È possibile contrassegnare i record per l'eliminazione tramite il driver, ma non è possibile rimuovere in modo permanente i record dal database. Per rimuovere definitivamente i record da una tabella, usare Visual FoxPro.  
  
## <a name="increasing-performance-using-background-fetching"></a>Miglioramento delle prestazioni tramite il recupero in Background  
 È possibile migliorare le prestazioni in recuperi di grandi dimensioni tramite lo sfondo il recupero di funzionalità del driver. Il recupero in background Usa un thread separato per recuperare i dati richiesti da un'origine dati specifica.  
  
 È possibile impiegare in background il recupero per un'origine dati in uno dei modi seguenti:  
  
-   Verificare i **recuperare i dati in background** casella di controllo la [nella finestra di dialogo programma di installazione di ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md).  
  
-   Usare la parola chiave attributi BackgroundFetch nella stringa di connessione.  
  
 Per informazioni sulle parole chiave attributo di stringa di connessione, vedere [uso di stringhe di connessione](../../odbc/microsoft/using-connection-strings.md).  
  
## <a name="updating-multitiered-views"></a>L'aggiornamento delle viste a più livelli  
 Una vista a più livelli è una vista basata su una o più visualizzazioni anziché su una tabella di base. Quando si esegue l'aggiornamento dati in una vista a più livelli, aggiornamenti scendere di un solo livello, per la visualizzazione su cui si basa la visualizzazione di primo livello; tabelle di base non vengono aggiornate.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>Uso di Data Definition Language (DDL) nelle Stored procedure  
 DDL, ad esempio CREATE TABLE o ALTER TABLE, è possibile usare nelle procedure di Visual FoxPro archiviati.  
  
 Per informazioni sul linguaggio, è possibile utilizzare in stored procedure, vedere [supporto per la Stored procedure, trigger, valori predefiniti e regole](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md).  
  
## <a name="using-positioned-updates"></a>Usando gli aggiornamenti posizionati  
 Il driver non supporta gli aggiornamenti posizionati. Utilizzare la clausola SQL WHERE per identificare le righe da aggiornare.  
  
## <a name="using-the-set-ansi-command"></a>Il comando SET ANSI  
 Se sei uno sviluppatore di Visual FoxPro, è necessario essere consapevoli che l'impostazione predefinita per SET ANSI è ON per il driver, a differenza di un'impostazione predefinita di OFF di Visual FoxPro. L'impostazione predefinita in impostazione per il SET ANSI consente a origini dati Visual FoxPro da un comportamento coerente con altre origini dati ODBC che in genere eseguono confronti esatti. È possibile modificare l'impostazione predefinita. Per altre informazioni, vedere [SET ANSI](../../odbc/microsoft/set-ansi-command.md).
